<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js App" />
    <!-- 子から親にイベントを渡す　$emit -->
    <ul>
    <comp-child
      v-for="item in list"
      v-bind:key="item.id"
      v-bind="item"
      @attack="handleAttack"/>
    </ul>
    <GetRepository/>
    <Chap2/>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import CompChild from "./components/CompChild.vue";
import GetRepository from "./components/GetRepository.vue";
import Chap2 from "./components/Chap2.vue";

export default {
  name: "app",
  components: {
    HelloWorld,
    CompChild,
    GetRepository,
    Chap2
  },
  data() {
    return {
      list: [
        { id: 1, name: "スライム", hp: 100 },
        { id: 2, name: "ドラゴン", hp: 100 },
        { id: 3, name: "ゴブリン", hp: 100 }
      ]
    };
  },
  methods: {
    handleAttack: function(id) {
      // findはES6〜
      const item = this.list.find(function(el) {
        return el.id === id;
      });
      if (item !== undefined && item.hp > 0) item.hp -= 10;
    }
  }
};
</script>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
