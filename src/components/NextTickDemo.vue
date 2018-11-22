<template>
<div>
  <p><button @click="getMessage" :disabled="isLoading">Get JSON</button> 各リストアイテムをクリックすると消えるよ！</p>
  <div id="box" :style="{height: boxHeight + 'px'}" :class="{loading: isLoading}">
    <div id="box-body" ref="body">
      <p v-for="(item, idx) in messages" @click="remove(idx)" :key="idx">{{ item }}</p>
    </div>
    <transition name="fade">
      <div class="overlay" v-show="isLoading"><span>LOADING NOW</span></div>
    </transition>
  </div>
  <p>BOXの高さ：{{ boxHeight }} px</p>
</div>
</template>

<script>
import axios from "axios";

export default {
  name: "NextTickDemo",
  data: function() {
    return {
      isLoading: false,
      messages: [],
      boxHeight: ""
    };
  },
  watch: {
    // messages に変化があったらする処理
    messages: function() {
      // DOMに反映された後に高さを取得
      this.$nextTick(function() {
        this.boxHeight = this.$refs.body.getBoundingClientRect().height;
      });
    }
  },
  methods: {
    // ajax で json データを取得して messages にセット
    // http://chibinowa.net/note/vuejs/vue-8.html
    getMessage: function() {
      var self = this;
      self.isLoading = true;

      axios
        .post("http://localhost:8000/1.php")
        .then(function(response) {
          self.messages = response.data.split(",");
        })
        .catch()
        .then(function() {
          self.isLoading = false;
        });
    },
    remove: function(idx) {
      this.messages.splice(idx, 1);
    }
  },
  mounted: function() {
    this.messages = ["no message"];
  }
};
</script>

<style lang="sass">
#box-body
  box-sizing: border-box
  width: 100%
  padding: 10px
  border: solid 1px 
</style>

