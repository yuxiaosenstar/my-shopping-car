<template>
  <div class="goods-container">
    <div class="goods-img">
      <input
        type="checkbox"
        class="custom-input"
        :checked="state"
        @change="stateChange"
      />
      <img :src="pic" alt="" />
    </div>
    <div class="goods-info">
      <div class="goods-title">{{ title }}</div>
      <div class="goods-info-bottom">
        <div class="goods-price">￥{{ price }}</div>
        <Counter :num="count" :id="id"></Counter>
      </div>
    </div>
  </div>
</template>

<script>
import Counter from "./Counter.vue";
export default {
  name: "Goods",
  props: {
    id: {
      required: true,
      type: Number,
    },
    title: {
      default: "",
      type: String,
    },
    pic: {
      default: "",
      type: String,
    },
    price: {
      default: 0,
      type: Number,
    },
    state: {
      default: true,
      type: Boolean,
    },
    count: {
      default: 1,
      type: Number,
    },
  },
  methods: {
    stateChange(e) {
      const newState = e.target.checked;
      this.$emit("state-change", { id: this.id, value: newState });
    },
  },
  components: {
    Counter,
  },
};
</script>

<style lang="less">
.goods-container {
  padding: 10px;
  display: flex;
  .goods-img {
    display: flex;
    align-items: center;
    img {
      width: 100px;
      height: 100px;
      margin: 0 10px;
    }
  }
  .goods-info {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    flex: 1;
    .goods-title {
      font-weight: bold;
      font-size: 12px;
    }
    .goods-info-bottom {
      display: flex;
      justify-content: space-between;
      .goods-price {
        font-weight: bold;
        color: red;
        font-size: 13px;
      }
    }
  }
}
</style>
