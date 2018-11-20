<template>
<div>
  <p>X: {{ halfPoint.x }}</p>
  <p>Y: {{ halfPoint.y }}</p>
  <input v-model.number="budget"> 円以下に絞り込む
  <input v-model.number="limit"> 件を表示
  <button v-on:click="order=!order">切り替え</button>
  <p>{{ matched.length }} 件中 {{ limited.length }} 件を表示中</p>
  <ul>
    <!-- v-forでは最終結果、算出プロパティのlimitedを使用する -->
    <li v-for="item in limited" v-bind:key="item.id">
      {{ item.name }} {{ item.price }}円
    </li>
  </ul>
  180 度は {{ 180 | radian | round }} ラジアンだよ
</div>
</template>

<script>
import _ from "lodash";

export default {
  name: "Chap3",
  data() {
    return {
      width: 800,
      height: 600,
      order: false,
      // フォームの入力と紐付けるデータ
      budget: 300,
      // 表示件数
      limit: 2,
      // もとになるリスト
      list: [
        { id: 1, name: "りんご", price: 100 },
        { id: 2, name: "ばなな", price: 200 },
        { id: 3, name: "いちご", price: 400 },
        { id: 4, name: "おれんじ", price: 300 },
        { id: 5, name: "めろん", price: 500 }
      ]
    };
  },
  computed: {
    halfWidth: function() {
      return this.width / 2;
    },
    halfHeight: function() {
      return this.height / 2;
    },
    // 「width × height」の中心座標をオブジェクトで返す
    halfPoint: function() {
      return {
        x: this.halfWidth,
        y: this.halfHeight
      };
    },
    // budget以下のリストを返す算出プロパティ
    matched: function() {
      // return this.list.filter(function(el) {
      //   return el.price <= this.budget;
      // }, this);
      return this.list.filter(el => el.price < this.budget);
    },
    sorted: function() {
      return _.orderBy(this.matched, "price", this.order ? "desc" : "asc");
    },
    // matchedで返ったデータをlimit件返す算出プロパティ
    limited: function() {
      return this.sorted.slice(0, this.limit);
    }
  },
  filters: {
    // 小数点以下を第2位に丸めるフィルタ
    round: function(val) {
      return Math.round(val * 100) / 100;
    },
    // 度からラジアンに変換するフィルタ
    radian: function(val) {
      return (val * Math.PI) / 180;
    }
  }
};
</script>

<style lang="sass">
</style>

