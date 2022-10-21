<template>
  <div class="app-container">
    <Header title="购物车"></Header>
    <Goods
      v-for="item in list"
      :key="item.id"
      :id="item.id"
      :title="item.goods_name"
      :pic="item.goods_img"
      :state="item.goods_state"
      :count="item.goods_count"
      :price="item.goods_price"
      @state-change="getNewState"
    ></Goods>
    <Footer
      :isFull="fullState"
      :all="total"
      :amount="amt"
      @full-change="getFullChange"
    ></Footer>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Goods from "./components/Goods.vue";
import Footer from "./components/Footer.vue";
import axios from "axios";
import bus from "./components/eventBus.js";

export default {
  name: "App",
  components: {
    Header,
    Goods,
    Footer,
  },
  data() {
    return {
      list: [],
    };
  },
  computed: {
    fullState() {
      return this.list.every((item) => item.goods_state);
    },
    amt() {
      return this.list
        .filter((item) => item.goods_state)
        .reduce((t, item) => (t += item.goods_price * item.goods_count), 0);
    },
    total() {
      return this.list
        .filter((item) => item.goods_state)
        .reduce((t, item) => (t += item.goods_count), 0);
    },
  },
  created() {
    this.initCartList();

    bus.$on("share", (val) => {
      this.list.some((item) => {
        if (item.id === val.id) {
          item.goods_count = val.value;
          return true;
        }
      });
    });
  },
  methods: {
    async initCartList() {
      const { data: res } = await axios.get("https://www.escook.cn/api/cart");
      if (res.status === 200) {
        this.list = res.list;
      }
    },
    getFullChange(val) {
      this.list.forEach((item) => (item.goods_state = val));
    },
    getNewState(e) {
      this.list.some((item) => {
        if (item.id === e.id) {
          item.goods_state = e.value;
          return true;
        }
      });
    },
  },
};
</script>

<style lang="less">
.app-container {
  padding-top: 45px;
  padding-bottom: 50px;
}
</style>
