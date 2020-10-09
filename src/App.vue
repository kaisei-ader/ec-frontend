<template>
  <div id="app">
    <header>
      <div class="header-wrap">
        <span>Neumorphism Ec Shop</span>
      </div>
    </header>
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <router-view />
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

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
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
