<template>
  <label class="scoped-wrap">
    <input @change="inputHandler" type="checkbox" v-model="val" />
    <div class="slider round">
      <span>{{ title }}</span>
    </div>
  </label>
</template>

<script>
export default {
  name: "Toggle",
  props: {
    value: [Boolean, String],
    title: String,
  },
  data() {
    return {
      val:
        typeof this.value === "boolean"
          ? this.value
          : !!(this.value == "true" || this.value == "on"),
    };
  },
  watch: {
    value(val) {
      this.val =
        typeof val == "string" ? !!(val == "true" || val == "on") : val;
    },
  },
  methods: {
    inputHandler() {
      this.$emit("input", this.val);
    },
  },
};
</script>

<style scoped>
:root {
  --bgl-blue: #2e5bff;
  --bgl-gray: #bfbfbf;
}
.scoped-wrap {
  position: relative;
  display: inline-block;
  width: 36px;
  height: 19px;
  user-select: none;
  transform: translate(30px, -2px);
  text-transform: capitalize;
}
.scoped-wrap span {
  position: absolute;
  left: calc(100% + 6px);
  top: 1px;
  color: #000000;
  font-size: 12px;
}
.scoped-wrap input {
  opacity: 0;
  width: 0;
  height: 0;
}

.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #d0d0d0;
  -webkit-transition: 0.4s;
  transition: 0.4s;
}

.slider:before {
  position: absolute;
  content: "";
  height: 13px;
  width: 13px;
  left: 4px;
  bottom: 3px;
  background-color: white;
  -webkit-transition: 0.4s;
  transition: 0.4s;
}

input:checked + .slider {
  background-color: #2e5bff;
}

input:focus + .slider {
  box-shadow: 0 0 1px #2e5bff;
}

input:checked + .slider:before {
  transform: translateX(16px);
}

.slider.round {
  border-radius: 34px;
}

.slider.round:before {
  border-radius: 50%;
}
</style>
