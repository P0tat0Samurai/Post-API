<template>
  <div class="home">
    <h1>郵便番号から該当地域を検索する</h1>
    <input
      v-model="postcode"
      type="text"
      maxlength="7"
      placeholder="郵便番号を入力"
    />
    <button @click="searchAdressInfo" type="submit">検索</button>
    <p>※ 3桁以上の数値を入力してください（例：1500001）</p>
    <h2>検索結果：{{ allAdress }}</h2>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      postcode: "",
      allAdress: "",
    };
  },
  methods: {
    async searchAdressInfo() {
      let item = await axios.get(
        `https://apis.postcode-jp.com/api/v4/postcodes/${this.postcode}?apiKey=QEX6w8u2EMpeZz2c49aFiwhJZOC0ftiH2ILV0Yr`
      );
      this.allAdress = item.data[0].allAddress;
    },
  },
};
</script>

<style scoped>
.home h1 {
  width: 50%;
  padding: 20px;
  margin-left: 10px;
  color: #CC0000;
  font-size: 18px;
  font-weight: bold;
  border-bottom: 4px solid #CC0000;
  border-width: 80%;
}
.home p, h2 {
  margin-left: 10px;
  padding: 10px;
}
input {
  padding: 5px;
  margin: 10px 5px 10px 20px;
}
button {
  padding: 2px 5px;
  background: #fff;
  color: #000;
}
button:hover {
  background: #000;
  color: #fff;
}
</style>