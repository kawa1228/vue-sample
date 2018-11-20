<template>
<div>
    <button v-on:click="handleClick">カウントアップ</button>
    <button v-on:click="show=!show">表示/非表示</button>
    <span ref="count" v-if="show">0</span>
    <p class="cloak" v-cloak>
      {{ message }}
    </p>
    <div v-on:click.right="handler">右クリック</div>
    <!-- 右ボタンを押した時のコンテキストメニューを表示させない -->
    <div v-on:click.right.prevent="handler">右クリック</div>
</div>
</template>
<script>
export default {
  name: "Chap2",
  data() {
    return {
      show: true,
      message: "ふわっと出てくる"
    };
  },
  methods: {
    handleClick() {
      var count = this.$refs.count;
      if (count) {
        count.innerText = parseInt(count.innerText, 10) + 1;
      }
    },
    handler: function() {
      console.log("押された");
    }
  }
};
</script>

<style lang="sass">
@keyframes cloak-in
  0%
    opacity: 0
.cloak
  animation: cloak-in 1s
.cloak[v-cloak]
  opacity: 0
</style>

