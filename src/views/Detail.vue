<template>
  <div class="detail">
    <span class="detail-title">商品詳細</span>
    <div class="detail-wrap">
      <div class="detail-img">
        <img :src="`http://127.0.0.1:8000/${product.path}`" />
      </div>
      <div class="detail-explain">
        <h2>{{ product.title }}</h2>
        <h3>{{ product.text }}</h3>
        <h1>￥{{ product.price }}</h1>
        <div class="flex">
          <span>数量 :</span>
          <select name="num" v-model="quantity">
            <option :value="n" v-for="n in 30" :key="n">{{ n }}</option>
          </select>
        </div>
        <button @click="carAdd" id="add-button">カートに追加</button>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "detail",
  data() {
    return {
      product: {},
      quantity: "1",
    };
  },
  created() {
    this.get();
  },
  methods: {
    carAdd() {
      axios
        .post(`${process.env.VUE_APP_API_URL}/api/carts`, {
          quantity: this.quantity,
          productId: this.$route.params.id,
        })
        .then(() => {
          this.$router.push("/cart");
        });
    },
    get() {
      axios
        .get(
          `${process.env.VUE_APP_API_URL}/api/products/${this.$route.params.id}`
        )
        .then((res) => {
          this.product = res.data;
        });
    },
  },
};
</script>
<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Noto+Sans+JP:wght@900&display=swap");
@import url("https://raw.githubusercontent.com/filipelinhares/ress/master/ress.css");

.detail {
  width: 75%;
  position: relative;
  .detail-title {
    position: absolute;
    top: 5%;
    left: 10%;
    font-size: 26px;
    color: rgba(82, 81, 81);
    font-family: "Noto Sans JP", sans-serif;
    border-bottom: 2px solid;
  }
  .detail-wrap {
    width: 90%;
    display: flex;
    justify-content: space-between;
    position: absolute;
    top: 20%;
    left: 10%;

    .detail-img {
      width: 40%;
      height: 400px;
      background: #e0e6ec;
      box-shadow: 7px 7px 14px #bec4c9, -7px -7px 14px #ffffff;

      img {
        width: 100%;
      }
    }
    .detail-explain {
      margin-top: 10px;
      display: flex;
      flex-direction: column;
      align-items: flex-start;
      width: 50%;
      color: rgba(82, 81, 81);
      font-family: "Noto Sans JP", sans-serif;

      h2 {
        font-size: 50px;
        margin-bottom: 30px;
      }

      h3 {
        font-size: 20px;
        margin-bottom: 30px;
      }

      h1 {
        display: block;
        margin-bottom: 30px;
        font-size: 40px;
        font-weight: 600;
        color: rgba(255, 0, 0, 0.6);
      }

      .flex {
        display: flex;
      }
      #add-button {
        padding: 20px 100px;
        border-radius: 20px;
        border: none;
        color: rgb(82, 81, 81);
        font-weight: 600;
        background: #e0e6ec;
        box-shadow: 7px 7px 14px #bec4c9, -7px -7px 14px #ffffff;
        cursor: pointer;
        font-family: "Noto Sans JP", sans-serif;
        transition: all 0.1s;

        &:focus {
          outline: 0;
        }

        &:active,
        &.active {
          outline: 0;
          box-shadow: none;
        }
      }
    }
  }
}
</style>
