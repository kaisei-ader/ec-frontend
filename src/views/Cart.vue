<template>
  <div class="cart">
    <div class="cart-title">
      <span>カートの中</span>
    </div>
    <div class="cart-items">
      <span>ご注文内容</span>
      <table>
        <tr>
          <th>商品画像</th>
          <th>商品名</th>
          <th>数量</th>
          <th>小計</th>
        </tr>
        <tr class="item" v-for="cart in carts" :key="cart.id">
          <td class="img">
            <img :src="`${apiUrl}/${cart.product.path}`" />
          </td>
          <td>{{ cart.product.title }}</td>
          <td>{{ cart.quantity }}</td>
          <td>{{ cart.quantity * cart.product.price }}</td>
          <td><button @click="() => remove(cart.id)">削除</button></td>
        </tr>
        <td>合計金額</td>
        <td></td>
        <td></td>
        <td>{{ this.amount }}</td>
        <td></td>
      </table>
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
      apiUrl: process.env.VUE_APP_API_URL,
    };
  },
  created() {
    this.get();
  },
  methods: {
    get() {
      Axios.get(`${process.env.VUE_APP_API_URL}/api/carts`).then((res) => {
        this.carts = res.data;
        this.totalAmount();
      });
    },
    remove(id) {
      Axios.delete(`${process.env.VUE_APP_API_URL}/api/carts/${id}`).then(
        () => {
          this.get();
        }
      );
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

    table {
      position: absolute;
      margin-top: 20px;
      top: 80%;
      left: -5%;
      border-collapse: collapse;
      border-spacing: 0;
      width: 90%;

      tr {
        border-bottom: solid 1px #eee;
        cursor: pointer;
      }

      th,
      td {
        text-align: center;
        width: 25%;
        padding: 15px 0;
      }

      .totall {
        color: rgba(82, 81, 81);
        font-family: "Noto Sans JP", sans-serif;
        font-size: 30px;
      }

      img {
        width: 100px;
      }
    }
  }
}
</style>