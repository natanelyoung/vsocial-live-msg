<template>
  <div class="queue-item" @click="emitdblclick">
    <div class="dot-wrap">
      <img src="../assets/dots.svg" height="" width="" class="dots" />
    </div>
    <p v-if="message.amount" class="amount">
      ${{ parseInt(message.amount).toLocaleString() }}
    </p>
    <div class="before-name" v-if="message.amount && message.name"></div>
    <p v-if="message.name" class="name">{{ message.name }}<br /></p>
    <p class="msg-txt">
      {{ message.message }}
    </p>
    <!-- <div v-if="idx == 0" class="progress-wrapper">
      <div
        class="progress"
        :style="{ width: (newMessageCounter / messageInterval) * 100 + '%' }"
      />
    </div> -->
  </div>
</template>

<script>
export default {
  name: "queue-item",
  props: {
    message: Object,
    idx: Number,
    messageInterval: Number,
    newMessageCounter: Number,
  },
  methods: {
    emitdblclick(event) {
      this.$emit("dblclick", event);
    },
  },
  watch: {
    messageInterval() {},
    newMessageCounter() {},
  },
};
</script>

<style scoped>
.progress-wrapper {
  position: absolute;
  height: 5px;
  bottom: 0;
  left: 0;
  right: 0;
}
.progress {
  height: 5px;
  width: 50%;
  background: blue;
  transition: width ease-in-out 0.5s;
}
.queue-item {
  border-radius: 10px;
  background: #f6f7f9;
  padding: 23px 23px 23px 40px;
  position: relative;
  margin-bottom: 20px;
  overflow: hidden;
}

.dot-wrap {
  width: 40px;
  height: 100%;
  text-align: center;
  position: absolute;
  top: 0;
  left: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: grab;
}

.dot-wrap:active {
  cursor: grabbing;
}

.amount {
  display: inline-block;
  font-size: 20px;
  font-weight: 700;
  margin: 0;
}
.before-name {
  height: 14px;
  background: black;
  width: 2px;
  display: inline-block;
  margin: 0 8px;
}

.name {
  display: inline-block;
  font-size: 20px;
  margin: 0;
}

.msg-txt {
  font-size: 16px;
  line-height: 1.6;
  margin: 6px 0 0 0;
}

.dots {
  width: 4px;
}
</style>