<template>
  <div class="header-container">{{ title }}</div>
</template>

<script>
export default {
  name: "Header",
  props: {
    title: {
      type: String,
      default: "",
    },
  },
};
</script>

<style>
.header-container {
  font-size: 12px;
  height: 45px;
  width: 100%;
  background-color: #1d7bff;
  display: flex;
  justify-content: center;
  align-items: center;
  color: #fff;
  position: fixed;
  top: 0;
}
</style>
