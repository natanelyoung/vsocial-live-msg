<template>
      <div class="incoming-msg"><p class="queued">Queued</p>
    <p class="amount">$100</p>
    <div class="before-name"></div>
    <p class="name">Nati</p><p class="msg-txt">Lorem ipsum dolor sit dkj doifv okdfjvk ndfskv ndsfv ikndfkvj ndfvjk dfnjkvnd fvkjndf vkjdnfjkv&nbsp;</p></div>
      </template>
      <script>
      export default {
          props: [],
          name: "msg"
      };
      </script>
        <style scoped="">.queued {
  color: #2E5BFF;
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
  filter: brightness(90%);
}

.incoming-msg {
  transition: all ease 200ms;
}</style>