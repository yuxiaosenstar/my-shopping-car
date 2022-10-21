<template>
  <div class="footer-container">
    <div class="custom-checkbox">
      <input type="checkbox" :checked="isFull" @change="fullChange" />
      <span>全选</span>
    </div>

    <div>
      <span>合计: </span>
      <span class="total-price">￥{{ amount.toFixed(2) }}</span>
    </div>

    <button class="btn-settle">结算{{ all }}</button>
  </div>
</template>

<script>
export default {
  name: "Footer",
  props: {
    isFull: {
      type: Boolean,
      default: true,
    },
    amount: {
      type: Number,
      default: 0,
    },
    all: {
      type: Number,
      default: 0,
    },
  },
  methods: {
    fullChange(e) {
      this.$emit("full-change", e.target.checked);
    },
  },
};
</script>

<style lang="less">
.footer-container {
  font-size: 12px;
  height: 50px;
  width: 100%;
  border-top: 1px solid #efefef;
  position: fixed;
  bottom: 0;
  background-color: #fff;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 10px;
}

.custom-checkbox {
  display: flex;
  align-items: center;
}

.total-price {
  font-weight: bold;
  font-size: 14px;
  color: red;
}

.btn-settle {
  height: 80%;
  min-width: 110px;
  border-radius: 25px;
  font-size: 12px;
  margin-right: 20px;
}
</style>
