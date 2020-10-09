<template>
  <div class="insert">
    <div class="insert-title">
      <span>新規商品を追加</span>
    </div>
    <div class="insert-box">
      <div class="item-flex">
        <span>商品名:</span
        ><input type="text" class="new-item-button" v-model="newItem" />
      </div>
      <div class="item-flex">
        <span>画像挿入:</span
        ><input type="file" id="file" @change="confirmImg" />
        <label for="file">ファイルを選択してください</label>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newItem: "",
      view: true,
    };
  },
};
</script>
<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Noto+Sans+JP:wght@900&display=swap");
@import url("https://raw.githubusercontent.com/filipelinhares/ress/master/ress.css");
.insert {
  width: 75%;
  position: relative;

  .insert-title {
    position: absolute;
    top: 5%;
    left: 10%;
    font-size: 26px;
    color: rgba(82, 81, 81);
    font-family: "Noto Sans JP", sans-serif;
    border-bottom: 2px solid;
  }

  .insert-box {
    position: absolute;
    top: 20%;
    left: 10%;
    display: flex;
    flex-direction: column;

    .item-flex {
      display: flex;
      align-items: center;
      margin-bottom: 30px;

      span {
        font-size: 28px;
        color: rgba(82, 81, 81);
        font-family: "Noto Sans JP", sans-serif;
      }

      input[type="file"] {
        display: none;
      }

      label {
        margin-left: 20px;
        background: #2928f5;
        opacity: 0.7;
        color: white;
        font-size: 0.8rem;
        padding: 6px 12px;
        border-radius: 4px;
        display: inline-block;
        position: relative;
        cursor: pointer;

        &:hover {
          opacity: 0.7;
          transition: 0.3s ease-out;
        }
      }
      .new-item-button {
        background: #e0e6ec;
        box-shadow: 7px 7px 14px #bec4c9, -7px -7px 14px #fff;
        margin-left: 10px;
        width: 600px;
        height: 50px;
        font-size: 23px;
        text-shadow: 1px 1px 1px #fff;
        box-sizing: border-box;
        outline: none;
        margin-left: 20px;
        padding: 20px;
        color: rgb(82, 81, 81);
        font-family: "Noto Sans JP", sans-serif;
        border-radius: 55px;
        border: 1px solid rgba(255, 255, 255, 0.6);
      }
    }
  }
}
</style>