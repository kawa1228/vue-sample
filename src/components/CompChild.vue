<!-- P163 親がもつデータを操作 -->
<template>
  <div>
    <li>
      {{ name }} HP.{{ hp }}
      <button @click="doAttack">attack</button>
    </li>
  </div>
</template>

<script>
export default {
  name: "CompChild",
  props: {
    id: Number,
    name: String,
    hp: Number
  },
  created: function() {
    this.$on("open", function() {
      console.log("hello");
    });
  },
  methods: {
    doAttack: function() {
      this.$emit("attack", this.id);
    }
  }
};
</script>
