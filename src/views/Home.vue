<template>
  <div class="home">
    <div class="shop-title">
      <span>商品一覧</span>
    </div>
    <div class="items">
      <div class="item" />
      <div class="item" />
      <div class="item" />
      <div class="item" />
      <div class="item" />
      <div class="item" />
    </div>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: "Home",
  components: {},
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
      height: 300px;
      margin-bottom: 40px;
      background: #e0e6ec;
      box-shadow: 7px 7px 14px #bec4c9, -7px -7px 14px #fff;
    }
  }
}
</style>