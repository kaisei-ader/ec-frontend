<template>
  <div class="home">
    <div class="shop-title">
      <span>商品一覧</span>
    </div>
    <div class="items">
      <div class="item" v-for="item in items" :key="item.id">
        <router-link :to="`/product/detail/${item.id}`">
          <img :src="'${process.env.VUE_APP_API_URL}/' + item.path" />
        </router-link>
        <span class="item-title">{{ item.title }}</span
        ><br />
        <span class="item-price">￥{{ item.price }}</span>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import axios from "axios";

export default {
  name: "Home",
  components: {},
  data() {
    return {
      items: [],
    };
  },
  created() {
    this.get();
  },
  methods: {
    get() {
      axios.get(`${process.env.VUE_APP_API_URL}/api/products/`).then((res) => {
        this.items = res.data;
      });
    },
  },
};
</script>

<style lang="scss">
.home {
  width: 75%;
  position: relative;
  .shop-title {
    position: absolute;
    top: 5%;
    left: 10%;
    font-size: 26px;
    color: rgba(82, 81, 81);
    font-family: "Noto Sans JP", sans-serif;
    border-bottom: 2px solid;
  }
  .items {
    position: absolute;
    top: 15%;
    left: 5%;
    width: 100%;
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;

    .item {
      width: 30%;
      margin-bottom: 40px;

      img {
        width: 100%;
        background: #e0e6ec;
        box-shadow: 7px 7px 14px #bec4c9, -7px -7px 14px #fff;
        margin-bottom: 15px;
      }
      .item-title {
        text-align: center;
        font-size: 20px;
        margin-top: 20px;
        color: rgba(82, 81, 81);
        font-family: "Noto Sans JP", sans-serif;
      }
      .item-price {
        text-align: center;
        font-size: 20px;
        font-weight: 600;
        margin-top: 20px;
        color: rgba(255, 0, 0, 0.6);
      }
    }
  }
}
</style>