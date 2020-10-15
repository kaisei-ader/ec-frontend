<template>
  <div class="insert">
    <div class="insert-title">
      <span>新規商品を追加</span>
    </div>
    <div class="insert-box">
      <div class="item-flex">
        <span>商品名:</span
        ><input type="text" class="new-item-button" v-model="newItem" />
        <div class="error">{{ message0 }}</div>
      </div>
      <div class="item-flex">
        <span>画像挿入 :</span
        ><input type="file" id="file" @change="confirmImg" v-if="view" />
        <label for="file">ファイルを選択してください</label>
        <div class="error">{{ message1 }}</div>
      </div>
      <div class="item-flex" v-if="confirmedImg">
        <img class="re-img" :src="confirmedImg" />
        <br />
        <div class="re-img-text">選択された画像です</div>
      </div>
      <div class="item-flex">
        <span>値段 :</span
        ><input type="number" class="new-price-button" v-model="newPrice" />
        <div class="new-price-alert">※半角数字のみを入力してください</div>
        <div class="error">{{ message2 }}</div>
      </div>
      <div class="item-flex">
        <span>商品概要 :</span>
        <textarea
          class="explain"
          name="kanso"
          cols="40"
          rows="4"
          maxlength="20"
          placeholder=" :商品の概要をご記入ください"
          v-model="newExplain"
        ></textarea>
        <div class="error">{{ message3 }}</div>
      </div>
      <div class="item-flex">
        <span>追加 :</span>
        <button @click="uploadImage" id="add-button">Add</button>
        <div class="error">{{ message4 }}</div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      newItem: "",
      newPrice: "",
      newExplain: "",
      file: "",
      confirmedImg: "",
      view: true,
      message0: "",
      message1: "",
      message2: "",
      message3: "",
      message4: "",
    };
  },
  methods: {
    confirmImg(e) {
      this.message = "";
      this.file = e.target.files[0];
      if (!this.file.type.match("image.*")) {
        this.message1 = "※画像ファイルを選択して下さい";
        this.confirmedImg = "";
        return;
      }
      this.createImg(this.file);
    },
    createImg(file) {
      let reader = new FileReader();
      reader.readAsDataURL(file);
      reader.onload = (e) => {
        this.confirmedImg = e.target.result;
      };
    },
    uploadImage() {
      let data = new FormData();
      if (
        this.newItem !== "" &&
        this.newPrice !== "" &&
        this.newExplain !== "" &&
        this.file !== ""
      ) {
        data.append("title", this.newItem);
        data.append("image", this.file);
        data.append("price", this.newPrice);
        data.append("text", this.newExplain);
        axios
          .post("http://127.0.0.1:8000/api/products", data, {
            headers: {
              "Content-Type": "mutlipart/form-data",
            },
          })
          .then(() => {
            this.$router.push("/");
          });
      } else {
        if (this.newItem === "") {
          this.message0 = "※商品名を入力してください";
        }
        if (this.file === "") {
          this.message1 = "※画像ファイルを選択して下さい";
        }
        if (this.newPrice === "") {
          this.message2 = "※値段を入力して下さい";
        }
        if (this.newExplain === "") {
          this.message3 = "※商品概要を入力して下さい";
        }
      }
    },
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
      .error {
        margin-left: 20px;
        font-size: 22px;
        color: red;
        font-family: "Noto Sans JP", sans-serif;
      }

      .re-img {
        width: 100px;
      }

      .re-img-text {
        margin-left: 20px;
        font-size: 16px;
        color: rgba(82, 81, 81);
        font-family: "Noto Sans JP", sans-serif;
      }

      .explain {
        font-size: 16px;
        padding: 20px;
        color: rgba(82, 81, 81);
        margin-left: 20px;
        font-family: "Noto Sans JP", sans-serif;
        border: none;
        border-radius: 10px;
        background: #e0e6ec;
        box-shadow: 7px 7px 14px #bec4c9, -7px -7px 14px #ffffff;
        outline: none;
      }

      input[type="file"] {
        display: none;
      }

      #add-button {
        padding: 10px 100px;
        border-radius: 20px;
        margin-left: 76px;
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
        width: 450px;
        height: 50px;
        font-size: 23px;
        text-shadow: 1px 1px 1px #fff;
        box-sizing: border-box;
        outline: none;
        margin-left: 50px;
        padding: 20px;
        color: rgb(82, 81, 81);
        font-family: "Noto Sans JP", sans-serif;
        border-radius: 55px;
        border: 1px solid rgba(255, 255, 255, 0.6);
      }

      .new-price-button {
        background: #e0e6ec;
        box-shadow: 7px 7px 14px #bec4c9, -7px -7px 14px #fff;
        width: 200px;
        height: 50px;
        font-size: 23px;
        text-shadow: 1px 1px 1px #fff;
        box-sizing: border-box;
        outline: none;
        margin-left: 70px;
        padding: 20px;
        color: rgb(82, 81, 81);
        font-family: "Noto Sans JP", sans-serif;
        border-radius: 55px;
        border: 1px solid rgba(255, 255, 255, 0.6);
      }

      .new-price-alert {
        margin-left: 20px;
        font-size: 16px;
        color: rgba(82, 81, 81);
        font-family: "Noto Sans JP", sans-serif;
      }
    }
  }
}
</style>