<template>
  <div class="home">
    <div class="total-amount">
      Total amount of donations:
      <span>${{ totalAmount.toLocaleString() }}</span>
    </div>
    <message-popup v-model="popupMessage" />
    <div class="main-box">
      <div class="side-wrap">
        <div class="head-wrap"><h1 class="head">Donations</h1></div>
        <div class="Incoming-msg-wrap">
          <msg
            v-for="donation of allDonations"
            :key="donation._id"
            :donation="donation"
            @click="popupMessage = donation"
          />
        </div>
      </div>
      <div class="queue-wrap">
        <h2 class="head">Message Queue</h2>
        <button
          @click="queueSettings.continuous = !queueSettings.continuous"
          :style="{
            'background-color':
              queueSettings.continuous === true ? '#2e5bff' : '#9699a5',
          }"
          class="continuous"
        >
          ⥀ Scroll Continuously ({{
            queueSettings.continuous === true ? "on" : "off"
          }})
        </button>
        <button class="playpause" @click="playPause(!queueSettings.playing)">
          {{ queueSettings.playing ? "||" : "▸" }}
        </button>
        <a @click="newMessage()" class="new-msg-btn"
          >New Custom Message<br
        /></a>

        <div class="queue-list-wrap">
          <draggable v-model="messageQueue" @sort="sort">
            <queue-item
              v-for="(message, i) of messageQueue"
              :key="message._id"
              :idx="i"
              :newMessageCounter="newMessageCounter"
              :messageInterval="messageInterval"
              :message="message"
              @dblclick="popupMessage = message"
            />
          </draggable>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import draggable from "vuedraggable";
import msg from "@/components/msg.vue";
import MessagePopup from "@/components/messagePopup.vue";
import QueueItem from "@/components/QueueItem.vue";
import Bagel from "@bageldb/bagel-db";
let db = new Bagel(process.env.VUE_APP_BAGEL_TOKEN);
export default {
  components: {
    msg,
    MessagePopup,
    QueueItem,
    draggable,
  },
  name: "Home",
  data() {
    return {
      allDonations: [],
      messageQueue: [],
      popupMessage: {},
      newMessageCounter: 0,
      messageInterval: 30,
      pause: true,
      queueSettings: {},
    };
  },
  async mounted() {
    let { data: messageQueue } = await db
      .collection("messageQueue")
      .sort("order")
      .get();
    this.messageQueue = messageQueue;
    db.collection("messageQueue").listen(
      (message) => {
        let { item, trigger, itemID } = JSON.parse(message.data);
        if (trigger == "update") {
          let idx = this.messageQueue.findIndex((i) => i._id == itemID);
          this.messageQueue.splice(idx, 1, item);
        }
        if (trigger == "delete")
          this.messageQueue = this.messageQueue.filter((i) => i._id != itemID);
        if (trigger == "create") this.messageQueue.push(item);
      },
      (err) => console.log(err)
    );

    let { data: donation } = await db.collection("donations").get();
    this.allDonations = donation;
    db.collection("donations").listen(
      (message) => {
        let { item, trigger, itemID } = JSON.parse(message.data);
        console.log(itemID);
        console.log(this.messageQueue);
        if (trigger == "delete")
          this.allDonations = this.allDonations.filter((i) => i._id != itemID);
        if (trigger == "create") this.allDonations.push(item);
        if (trigger == "update") {
          let idx = this.allDonations.findIndex((i) => i._id == itemID);
          this.allDonations.splice(idx, 1, item);
        }
      },
      (err) => console.log(err)
    );

    let { data: queueSettings } = await db
      .collection("messageQueueSettings")
      .get();
    this.queueSettings = queueSettings[0];

    db.collection("messageQueueSettings").listen(
      (message) => {
        let { item, trigger } = JSON.parse(message.data);
        if (trigger == "update") {
          this.queueSettings = item;
        }
      },
      (err) => console.log(err)
    );
  },
  computed: {
    totalAmount() {
      return this.allDonations.reduce(
        (acc, cur) => acc + parseFloat(cur?.amount) || 0,
        0
      );
    },
  },
  methods: {
    sort(e) {
      let item = this.messageQueue[e.newIndex];
      db.collection("messageQueue").item(item._id).put({ order: e.newIndex });
      // console.log(e);
    },
    playPause(playing) {
      db.collection("messageQueueSettings")
        .item(this.queueSettings._id)
        .put({ playing });
    },
    sendNewMessage() {
      let addSeconds = () => {
        this.newMessageCounter++;
        if (this.newMessageCounter >= this.messageInterval) {
          this.newMessageCounter = 0;
          this.sendNewMessage();
        }
        if (!this.pause) setTimeout(() => addSeconds(), 1000);
      };
      addSeconds();
    },
    addNewMessage(event) {
      this.messageQueue.push(event);
    },
    newMessage() {
      this.popupMessage = null;
      this.popupMessage = {
        newMessage: true,
      };
    },
  },
};
</script>

<style scoped="">
.total-amount {
  position: absolute;
  bottom: 4vw;
  font-size: 20px;
}
.total-amount span {
  font-weight: 600;
}

.continuous {
  position: absolute;
  top: 33px;
  right: 300px;
  color: white;
  border-radius: 100px;
  height: 32px;
  padding-right: 15px;
  padding-left: 15px;
}
.playpause {
  position: absolute;
  top: 33px;
  right: 251px;
  background: #2e5bff;
  color: white;
  border-radius: 100px;
  height: 32px;
  width: 32px;
}
.home {
  background: #f6f7f9;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  font-family: "Montserrat", sans-serif;
}

.main-box {
  border-radius: 20px;
  box-shadow: 0 0 30px #00000022;
  background: white;
  min-height: 300px;
  width: 90%;
  max-width: 1200px;
  overflow: hidden;
  display: flex;
  align-items: stretch;
  height: 80vh;
  margin-bottom: 4vh;
}

.side-wrap {
  background: #fbfcfc;
  width: 340px;
  flex-shrink: 0;
  border-right: 1px solid #f2f2f2;
}

.queue-wrap {
  flex-grow: 1;
  padding: 0 45px;
  position: relative;
}

.head {
  font-size: 22px;
  margin: 30px 0;
}

.head-wrap {
  padding: 0 30px;
}

.Incoming-msg-wrap {
  overflow: auto;
  height: calc(100% - 90px);
}

.incoming-msg {
  padding: 15px 30px 20px 30px;
  border-top: 1px solid #f0f0f0;
}

.queued {
  color: #2e5bff;
  font-size: 14px;
  line-height: 1;
  margin: 0;
}

.new-msg-btn {
  position: absolute;
  top: 30px;
  right: 40px;
  background: #2e5bff;
  color: white;
  border-radius: 30px;
  text-decoration: none;
  transition: 200ms all ease;
  font-size: 14px;
  padding: 8px 20px;
}

.new-msg-btn:hover {
  filter: brightness(90%);
}

.queue-list-wrap {
  height: calc(100% - 90px);
  overflow: auto;
}

.dot {
  height: 3px;
  width: 3px;
  background: black;
  border-radius: 100%;
  box-sizing: border-box;
  margin-bottom: 3px;
}

.queue-item:hover {
  filter: brightness(95%);
  cursor: pointer;
}
</style>
