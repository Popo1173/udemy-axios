<template>
  <div id="app">
    <h3>掲示板に投稿する</h3>
    <label for="name">ニックネーム</label>
    <input id="name" v-model="name" type="text">
    <br /><br />
    <label for="comment">コメント</label>
    <textarea id="comment" v-model="comment"></textarea>
    <br /><br />
    <button @click="createComment">コメントをサーバーに送る</button>
    <h2>掲示板</h2>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data () {
    return {
      name: "",
      comment: "",
    };
  },
  methods: {
    //非同期の処理
    createComment() {
      //postメソッド 第一引数:postするURL,第二引数はデータをオブジェクト、第三引数はオプション
      axios.post(
        'https://firestore.googleapis.com/v1/projects/vuejs-http-d2ba0/databases/(default)/documents/cities/comments',
        {
          //オブジェクト（ファイヤーベースの形式で送る
          fields: {
            name: {
              stringValue: this.name
            },
            comment: {
              stringValue: this.comment
            }
          }
        }
      )
      //postした結果を返す
      .then(response => {
        console.log(response);
      })
      //エラーの場合
      .catch(error => {
        console.log(error);
      });
    this.name ="";
    this.comment ="";
    }
  }
}
</script>


<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
