<template>
  <div id="app">
    <header>
      <div class="header-wrap">
        <span>Neumorphism Ec Shop</span>
      </div>
    </header>
    <div class="main">
      <div id="nav">
        <router-link to="/" class="shop">商品一覧</router-link>
        <router-link to="/cart" class="shop">カートの中</router-link>
        <router-link to="/product/add" class="shop">新規商品を追加</router-link>
      </div>
      <router-view />
    </div>
  </div>
</template>

<style lang="scss">
@charset "utf-8";
@import url("https://fonts.googleapis.com/css2?family=Noto+Sans+JP:wght@900&display=swap");
@import url("https://raw.githubusercontent.com/filipelinhares/ress/master/ress.css");

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.main {
  width: 100%;
  display: flex;
  #nav {
    margin-top: 30px;
    width: 15%;
    height: 100vh;
    border-radius: 0 30px 0 0;
    padding: 30px;
    display: flex;
    flex-direction: column;
    background: #e0e6ec;
    box-shadow: 7px 7px 14px #bec4c9, -7px -7px 14px #fff;

    .shop {
      background: #e0e6ec;
      box-shadow: 7px 7px 14px #bec4c9, -7px -7px 14px #fff;
      margin-bottom: 30px;
    }

    a {
      font-weight: bold;
      text-decoration: none;
      color: #2c3e50;

      &.router-link-exact-active {
        color: #2928f5;
        opacity: 0.7;
      }
    }
  }
}

* {
  padding: 0;
  margin: 0;
}

body {
  background: #e0e6ec;
}
header {
  width: 100%;
  height: 80px;
  z-index: 9;

  .header-wrap {
    width: 96%;
    height: 80px;
    margin: 0 auto;
    border-radius: 0 0 35px 35px;
    background: #e0e6ec;
    box-shadow: 7px 7px 14px #bec4c9, -7px -7px 14px #fff;
    display: flex;
    justify-content: center;
    align-items: center;

    span {
      text-align: center;
      font-size: 26px;
      color: rgba(82, 81, 81);
      font-family: "Noto Sans JP", sans-serif;
    }
  }
}
</style>
