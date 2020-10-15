<template>
  <div class="cart">
    <div class="cart-title">
      <span>カートの中</span>
    </div>
    <div class="cart-items">
      <span>ご注文内容</span>
      <div class="item" v-for="cart in carts" :key="cart.id">
        <img :src="'http://127.0.0.1:8000/' + cart.product.path" />
        <p>{{ cart.product.title }}</p>
        <p>{{ cart.product.price }}</p>
        <p>{{ cart.quantity }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import Axios from "axios";
export default {
  name: "cart",
  data() {
    return {
      carts: [],
    };
  },
  created() {
    this.get();
  },
  methods: {
    get() {
      Axios.get("http://127.0.0.1:8000/api/carts").then((res) => {
        this.carts = res.data;
      });
    },
  },
};
</script>
<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Noto+Sans+JP:wght@900&display=swap");
@import url("https://raw.githubusercontent.com/filipelinhares/ress/master/ress.css");

.cart {
  width: 75%;
  position: relative;
  .cart-title {
    position: absolute;
    top: 5%;
    left: 10%;
    font-size: 26px;
    color: rgba(82, 81, 81);
    font-family: "Noto Sans JP", sans-serif;
    border-bottom: 2px solid;
  }
  .cart-items {
    width: 90%;
    position: absolute;
    top: 20%;
    left: 10%;
    display: flex;
    flex-direction: column;

    span {
      width: 90%;
      height: 30px;
      color: rgba(82, 81, 81);
      font-family: "Noto Sans JP", sans-serif;
      background: #e0e6ec;
      box-shadow: 7px 7px 14px #bec4c9, -7px -7px 14px #ffffff;
    }
  }
}
</style>