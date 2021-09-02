<template>
  <!-- wrapper -->
  <div ref="BScroll" :style="wrapperStyle">
    <!-- content  高度要比wrapper高-->
    <div :style="contentStyle">
      <!-- for 循环实体 -->
      <slot></slot>
    </div>
  </div>
</template>
<script>
import BScroll from "@better-scroll/core"
import MouseWheel from "@better-scroll/mouse-wheel"
import ScrollBar from "@better-scroll/scroll-bar"
import lodash from "lodash"
BScroll.use(ScrollBar) // 滚动条
BScroll.use(MouseWheel) // 滚轮
export default {
  mounted() {
    console.log("看看是啥options", this.options, 1213123)
    this.$nextTick(() => {
      this.scroll = new BScroll(this.$refs.BScroll, {
        ...this.defaultOptions,
        ...this.options,
      })
    })
    window.onresize = lodash.debounce(() => {
      console.log(1111)
      this.scroll.refresh()
    }, 500)
    console.log(this.$slots, this.options.scrollX, 989992992929)
  },
  updated() {
    this.scroll.refresh()
    if (this.scroll && this.activeClass) {
      this.$nextTick(() => {
        this.scroll.scrollToElement(
          "." + this.activeClass,
          500,
          this.options.scrollX,
          true
        )
      })
    }
  },
  props: {
    options: {
      type: Object,
      default: () => {
        return {}
      },
    },
    wrapperStyle: { type: String, default: "" },
    contentStyle: { type: String, default: "" },
    activeClass: { type: String, default: "" },
  },
  data() {
    return {
      defaultOptions: { click: true, mouseWheel: true, scrollbar: false },
    }
  },
}
</script>
