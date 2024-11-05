<template>
  <div class="chatgpt-assist-app container">
    <h1 class="title">プロンプトヘルパー</h1>

    <!-- 目的選択セレクトボックス -->
    <div class="field">
      <label class="label" for="purpose">目的:</label>
      <div class="control">
        <div class="select is-fullwidth">
          <select v-model="selectedPurpose" id="purpose">
            <option v-for="option in purposes" :key="option" :value="option">{{ option }}</option>
          </select>
        </div>
      </div>
    </div>

    <!-- 入力欄 -->
    <div class="field">
      <label class="label" for="inputText">入力:</label>
      <div class="control">
        <textarea class="textarea" v-model="inputText" id="inputText" rows="4"></textarea>
      </div>
    </div>

    <!-- 投稿ボタン -->
    <div class="field">
      <div class="control">
        <button class="button is-primary is-fullwidth" @click="submitInput">投稿</button>
      </div>
    </div>

    <!-- 履歴＆出力エリア -->
    <div class="output-area">
      <h3 class="title is-5">履歴</h3>
      <ul>
        <li v-for="(entry, index) in history.slice().reverse()" :key="index" class="box">
          {{ entry.text }}
          <button class="button is-small is-link is-outlined" @click="copyToClipboard(entry.text)">
            <i class="fas fa-copy"></i>
          </button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      purposes: ["目的1", "目的2", "目的3"], // 目的リスト
      selectedPurpose: "",
      inputText: "",
      history: []
    };
  },
  methods: {
    submitInput() {
      if (this.inputText.trim()) {
        this.history.push({ text: this.inputText });
        this.inputText = "";
      }
    },
    copyToClipboard(text) {
      navigator.clipboard.writeText(text).then(() => {
        alert("コピーしました！");
      });
    }
  }
};
</script>

<style scoped>
@import "https://cdnjs.cloudflare.com/ajax/libs/bulma/0.9.3/css/bulma.min.css";
@import "https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css";

.chatgpt-assist-app {
  max-width: 600px;
  margin: 0 auto;
  padding-top: 20px;
}

.output-area {
  margin-top: 20px;
}
</style>
