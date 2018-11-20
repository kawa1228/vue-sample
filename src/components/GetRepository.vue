<!-- P133 ウォッチャ　-->
<template>
  <div class="get-repository">
    選択してね
    <select v-model="current">
      <option v-for="topic in topics" :key="topic.id" v-bind:value="topic.value">
        {{ topic.name }}
      </option>
    </select>
    <div v-for="(item, id) in list" :key="id">{{ item.full_name }}</div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "GetRepository",
  data() {
    return {
      list: [],
      current: "",
      topics: [
        { id: 1, value: "vue", name: "Vue.js" },
        { id: 2, value: "jQuery", name: "jQuery" }
      ]
    };
  },
  watch: {
    current: function(val) {
      axios
        .get("https://api.github.com/search/repositories", {
          params: { q: "topic:" + val }
        })
        .then(
          function(res) {
            this.list = res.data.items;
          }.bind(this)
        );
    }
  }
};
</script>

