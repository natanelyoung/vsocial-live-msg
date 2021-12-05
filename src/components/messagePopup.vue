<template>
  <div class="popup-wrap" :class="{ show: show && !hide }">
    <div class="popup">
      <h3 class="pop-head">Messages Info</h3>
      <input
        placeholder="Amount"
        v-model="content.amount"
        type="number"
        class="field"
      />
      <input
        placeholder="Name"
        v-model="content.name"
        type="text"
        class="field"
      />
      <textarea v-model="content.message" class="field"></textarea>
      <toggle
        v-if="content.approved !== undefined"
        title="Approved"
        v-model="content.approved"
        @input="approve"
      />
      <div class="popup-btns-wrap">
        <a
          v-if="content.approved !== undefined || content.newMessage"
          @click="addToQueue"
          class="popup-btn"
          >Add to Queue</a
        >
        <a v-else @click="save" class="popup-btn">Save</a>
        <div
          v-if="content._id && content.approved == undefined"
          @click="remove"
          href=""
          class="popup-btn remove"
        >
          Remove from Queue
        </div>
        <a @click="closePopup" href="" class="cancel">Cancel</a>
      </div>
    </div>
    <div class="background" @click="closePopup" />
  </div>
</template>

<script>
import Bagel from "@bageldb/bagel-db";
import Toggle from "./Toggle.vue";
let db = new Bagel(process.env.VUE_APP_BAGEL_TOKEN);
export default {
  components: { Toggle },
  name: "message-popup",
  props: {
    value: Object,
  },
  data() {
    return {
      content: {
        amount: "",
        name: "",
        message: "",
      },
      show: false,
      hide: false,
    };
  },
  methods: {
    closePopup() {
      this.hide = true;

      this.content = {};
      this.$emit("input", this.content);
      setTimeout(() => {
        this.show = false;
        this.hide = false;
      }, 100);
    },
    async remove() {
      await db.collection("messageQueue").item(this.content._id).delete();
      this.closePopup();
    },
    async save() {
      await db
        .collection("messageQueue")
        .item(this.content._id)
        .put(this.content);
      this.closePopup();
    },
    async addToQueue() {
      await db.collection("messageQueue").post(this.content);
      this.closePopup();
    },
    async approve(val) {
      await db
        .collection("donations")
        .item(this.content._id)
        .put({ approved: val });
    },
  },
  watch: {
    value: {
      deep: true,
      handler(val) {
        var contnet = Object.assign({}, val);
        if (contnet.anonymous == true) contnet.name = "Anonymous";
        this.content = contnet;
        this.show = true;
      },
    },
    content: {
      deep: true,
      handler(val) {
        if (val) this.show = true;
      },
    },
  },
};
</script>


<style scoped>
.popup-wrap {
  position: fixed;
  top: 0;
  right: 0;
  left: 0;
  bottom: 0;
  z-index: 9;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: 200ms ease all;
  display: none;
}

.popup-wrap .background {
  background: #00000020;
  position: fixed;
  top: 0;
  right: 0;
  left: 0;
  bottom: 0;
}

.popup {
  z-index: 2;
  background: white;
  padding: 40px 50px;
  border-radius: 10px;
  box-shadow: 0 0 30px #00000020;
  zoom: 0.2;
  opacity: 0;
  transition: all ease-in-out 0.3s;
}

.show .popup {
  zoom: 1;
  opacity: 1;
}

.pop-head {
  margin: 0 0 20px 0;
}

.field {
  display: block;
  padding: 15px;
  border-radius: 5px;
  margin-bottom: 10px;
  border: 1px solid #dcdddf;
  font-size: 16px;
  min-width: 400px;
  width: 100%;
}

.popup-btns-wrap {
  margin-top: 20px;
  font-size: 14px;
}

.popup-btn {
  text-align: center;
  text-decoration: none;
  border-radius: 30px;
  padding: 9px 15px;
  color: white;
  background: #2e5bff;
  transition: all ease 200ms;
}

.popup-btn.remove {
  background: #ca3a3a;
  margin-left: 20px;
  display: inline-block;
  cursor: pointer;
}

.popup-btn:hover {
  filter: brightness(90%);
}

.popup-wrap.show {
  display: flex;
  opacity: 1;
}

.cancel {
  float: right;
  color: black;
  margin-top: 8px;
  margin-left: 20px;
}
</style>