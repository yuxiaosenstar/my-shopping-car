<template>
  <div class="number-container">
    <button class="sub" @click="sub">-</button>
    <span class="number-box">{{ num }}</span>
    <button class="add" @click="add">+</button>
  </div>
</template>

<script>
import bus from "./eventBus.js";
export default {
  name: "Counter",
  props: {
    id: {
      type: Number,
      required: true,
    },
    num: {
      type: Number,
      default: 1,
    },
  },
  methods: {
    sub() {
      if (this.num - 1 === 0) return;
      const obj = { id: this.id, value: this.num - 1 };
      bus.$emit("share", obj);
    },
    add() {
      const obj = { id: this.id, value: this.num + 1 };
      bus.$emit("share", obj);
    },
  },
};
</script>
