<!-- du-alert 仅用于 this.$du-alert -->
<!-- 提供属性 -->
<!-- title -->
<!-- message -->
<!-- onClose -->

<template>
  <!-- v-if="show" -->
  <div class="messageWrapper">
    <div
      v-if="show"
      style="
        height: 30px;
        line-height: 30px;
        padding: 12px 30px;
        word-break: break-word;
        border-radius: 5px;
        text-align: center;
        font-size: larger;
      "
      :style="typeStyle"
    >
      {{ message }}
      <div
        @click="close"
        style="position: absolute; top: 0; bottom: 0; right: 10px; margin: auto"
        class="du-_close"
      ></div>
    </div>
  </div>
</template>
<script>
export default {
  props: {},
  components: {},
  created() {},
  data() {
    return {
      show: false,
      message: "",
      type: "info",
      duration: 3000, // 默认3秒消失
    }
  },
  computed: {
    typeStyle() {
      let style = {
        info: { "background-color": "#f6f6f6" },
        success: { "background-color": "#f0f9eb", color: "#67c23a" },
        error: { "background-color": "#fef0f0", color: "red" },
      }
      return style[this.type]
    },
  },
  methods: {
    close() {
      this.show = false
      // this.$destroy(true)
      // this.$el.parentNode.removeChild(this.$el)
    },
  },
  mounted() {
    setTimeout(() => {
      this.close() // 3000ms之后调用关闭方法
    }, this.duration)
  },
}
</script>
<style scoped>
.messageWrapper {
  animation: slideInDown;
  animation-duration: 0.3s;
  position: fixed;
  top: 20px;
  left: 0;
  right: 0;
  margin: auto;
  max-width: 40vw;
}
</style>
