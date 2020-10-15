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
        <p>{{ cart.quantity }}</p>
        <p>{{ cart.quantity * cart.product.price }}</p>
        <button @click="() => remove(cart.id)">削除</button>
      </div>
      <p v-if="amount !== 0">{{ this.amount }}</p>
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
      amount: 0,
    };
  },
  created() {
    this.get();
  },
  methods: {
    get() {
      Axios.get("http://127.0.0.1:8000/api/carts").then((res) => {
        this.carts = res.data;
        this.totalAmount();
      });
    },
    remove(id) {
      Axios.delete(`http://127.0.0.1:8000/api/carts/${id}`).then(() => {
        this.get();
      });
    },
    totalAmount() {
      this.amount = 0;
      this.carts.forEach((value) => {
        this.amount += value.quantity * value.product.price;
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