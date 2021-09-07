<!-- u1_loading 仅用于 this.$u1_loading -->
<!-- 提供属性 -->
<!-- load -->
<!-- close -->

<template>
  <div
    class="u1__modalWrapper"
    v-if="show"
    style="background-color: transparent;"
  >
    <div class="loading">
      <span></span>
      <span></span>
      <span></span>
      <span></span>
      <span></span>
    </div>
  </div>
</template>
<script>
import lodash from "lodash"
export default {
  props: {},
  components: {},
  created() {},
  data() {
    this.close = lodash.debounce(this.closeMethod, 0.78 * 1000)
    return {
      show: false,
    }
  },
  methods: {
    closeMethod() {
      this.show = false
    },
  },
}
</script>
<style scoped>
.loading {
  height: 40px;
}
.loading span {
  display: inline-block;
  margin: 0px 5px;
  width: 10px;
  border-radius: 4px;
  background: #31c6fc;
  animation: loading 1.04s ease infinite;
}
@keyframes loading {
  0%,
  100% {
    height: 40px;
    background: #31c6fc;
  }
  50% {
    height: 60px;
    margin-top: -20px;
    background: #40a4fa;
  }
}
.loading span:nth-child(2) {
  animation-delay: 0.13s;
}
.loading span:nth-child(3) {
  animation-delay: 0.26s;
}
.loading span:nth-child(4) {
  animation-delay: 0.39s;
}
.loading span:nth-child(5) {
  animation-delay: 0.52s;
}
</style>
