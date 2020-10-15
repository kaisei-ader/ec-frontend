<template>
  <div class="detail">
    <span class="detail-title">商品詳細</span>
    <div class="detail-wrap">
      <div class="detail-img">
        <img />
      </div>
      <div class="detail-explain">
        <h2>商品名: {{ product.title }}</h2>
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
      product: [],
    };
  },
  created() {
    this.get();
  },
  methods: {
    get() {
      axios
        .get("`http://127.0.0.1:8000/api/products/${this.$router.params.id`")
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
    }
    .detail-explain {
      width: 50%;
      font-size: 16px;
      color: rgba(82, 81, 81);
      font-family: "Noto Sans JP", sans-serif;
      text-align: left;
    }
  }
}
</style>
