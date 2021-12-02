<template>
  <div class="home"><div class="popup-wrap show">
    <div class="popup">
    <h3 class="pop-head">Messages Info</h3>
    <input
        placeholder="Amount"
        type="number"
        class="field"
     />
    <input
        placeholder="Name"
        type="text"
        class="field"
     /><textarea class="field"></textarea><div class="popup-btns-wrap"><a
    href=""
    class="popup-btn"
>Approve Add to Queue</a>
    <a
        href=""
        class="popup-btn remove"
    >Remove from Queue</a>
    <a
        href=""
        class="cancel"
    >Cancel</a></div></div></div>
  <div class="main-box"><div class="side-wrap">
    <div class="head-wrap"><h1 class="head">Incoming messages</h1></div>
    <div class="Incoming-msg-wrap"><msg></msg><msg></msg><msg></msg><msg></msg><msg></msg></div></div>
    <div class="queue-wrap"><h2 class="head">Message Queue</h2><a
                                       href=""
                                       class="new-msg-btn"
                                   >New Custom Message<br /></a>
    <div class="queue-list-wrap"><div class="queue-item"><div class="dot-wrap"><img
    src="../assets/dots.svg"
    height=""
    width=""
    class="dots"
 /></div>
    <p class="amount">$100</p>
    <div class="before-name"></div>
    <p class="name">Jon Moe<br /></p>
    <p class="msg-txt">Lorem ipsum dolor sit amet Lorem ipsum dolor sit amet Lorem ipsum dolor sit amet Lorem ipsum dolor sit amet Lorem&nbsp;</p></div><div class="queue-item"><div class="dot-wrap"><img
    src="../assets/dots.svg"
    height=""
    width=""
    class="dots"
 /></div>
    <p class="amount">$100</p>
    <div class="before-name"></div>
    <p class="name">Jon Moe<br /></p>
    <p class="msg-txt">Lorem ipsum dolor sit amet</p></div><div class="queue-item"><div class="dot-wrap"><img
    src="../assets/dots.svg"
    height=""
    width=""
    class="dots"
 /></div>
    <p class="amount">$100</p>
    <div class="before-name"></div>
    <p class="name">Jon Moe<br /></p>
    <p class="msg-txt">Lorem ipsum dolor sit amet</p></div><div class="queue-item"><div class="dot-wrap"><img
    src="../assets/dots.svg"
    height=""
    width=""
    class="dots"
 /></div>
    <p class="amount">$100</p>
    <div class="before-name"></div>
    <p class="name">Jon Moe<br /></p>
    <p class="msg-txt">Lorem ipsum dolor sit amet</p></div><div class="queue-item"><div class="dot-wrap"><img
    src="../assets/dots.svg"
    height=""
    width=""
    class="dots"
 /></div>
    <p class="amount">$100</p>
    <div class="before-name"></div>
    <p class="name">Jon Moe<br /></p>
    <p class="msg-txt">Lorem ipsum dolor sit amet</p></div><div class="queue-item"><div class="dot-wrap"><img
    src="../assets/dots.svg"
    height=""
    width=""
    class="dots"
 /></div>
    <p class="amount">$100</p>
    <div class="before-name"></div>
    <p class="name">Jon Moe<br /></p>
    <p class="msg-txt">Lorem ipsum dolor sit amet</p></div><div class="queue-item"><div class="dot-wrap"><img
    src="../assets/dots.svg"
    height=""
    width=""
    class="dots"
 /></div>
    <p class="amount">$100</p>
    <div class="before-name"></div>
    <p class="name">Jon Moe<br /></p>
    <p class="msg-txt">Lorem ipsum dolor sit amet</p></div></div></div></div>
  </div>
</template>

<script>
import msg from '@/components/msg.vue';
export default {
    components: {
        msg
    },
    name: 'Home'
};
</script>

        <style scoped="">.home {
  background: #F6F7F9;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  font-family: 'Montserrat', sans-serif;
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
  height: 90vh;
}

.side-wrap {
  background: #FBFCFC;
  width: 340px;
  flex-shrink: 0;
  border-right: 1px solid #F2F2F2;
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
  border-top: 1px solid #F0F0F0;
}

.queued {
  color: #2E5BFF;
  font-size: 14px;
  line-height: 1;
  margin: 0;
}

.new-msg-btn {
  position: absolute;
  top: 30px;
  right: 40px;
  background: #2E5BFF;
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

.queue-item {
  border-radius: 10px;
  background: #F6F7F9;
  padding: 23px 23px 23px 40px;
  position: relative;
  margin-bottom: 20px;
}

.dots {
  width: 4px;
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
  margin: 6px 0 0 0;
}

.queue-item:hover {
  filter: brightness(95%);
  cursor: pointer;
}

.popup-wrap {
  position: fixed;
  top: 0;
  right: 0;
  left: 0;
  bottom: 0;
  z-index: 9;
  align-items: center;
  justify-content: center;
  background: #00000020;
  opacity: 0;
  display: none ;
  transition: 200ms ease all;
}

.popup {
  background: white;
  padding: 40px 50px;
  border-radius: 10px;
  box-shadow: 0 0 30px #00000020;
}

.field {
  display: block;
  padding: 15px;
  border-radius: 5px;
  margin-bottom: 10px;
  border: 1px solid #DCDDDF;
  font-size: 16px;
  min-width: 400px;
  width: 100%;
}

.pop-head {
  margin: 0 0 20px 0;
}

.cancel {
  float: right;
  color: black;
  margin-top: 8px;
  margin-left: 20px;
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
  background: #2E5BFF;
  transform: all ease 200ms;
}

.popup-btn.remove {
  background: #CA3A3A;
  margin-left: 20px;
}

.popup-btn:hover {
  filter: brightness(90%);
}

.popup-wrap.show {
  display: flex ;
  opacity: 1;
}</style>