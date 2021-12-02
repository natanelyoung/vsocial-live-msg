<template>
  <div class="incoming-msg" @click="emitClick">
    <p v-if="donation.approved" class="queued">Approved</p>
    <p v-if="donation.amount" class="amount">
      ${{ donation.amount.toLocaleString() }}
    </p>
    <div class="before-name" v-if="donation.message && donation.amount"></div>
    <p class="name">{{ donation.message }}</p>
    <p class="msg-txt">
      {{ donation.name }}
    </p>
  </div>
</template>

<script>

export default {
  props: { donation: Object },
  name: "msg",
  methods:{
    emitClick(){
      this.$emit("click")
    }
  },
};
</script>

<style scoped="">
.queued {
  color: #2e5bff;
  margin: 0 0 10px 0;
}

.amount {
  display: inline-block;
  font-size: 20px;
  font-weight: 700;
  margin: 0;
}

.name {
  display: inline-block;
  font-size: 20px;
  margin: 0;
}

.before-name {
  height: 14px;
  background: black;
  width: 2px;
  display: inline-block;
  margin: 0 8px;
}

.msg-txt {
  font-size: 16px;
  line-height: 1.6;
  margin: 10px 0 0 0;
}

.incoming-msg:hover {
  filter: brightness(80%);
}

.incoming-msg {
  cursor: pointer;
  transition: all ease 200ms;
}
</style>