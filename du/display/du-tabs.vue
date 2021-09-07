<template>
  <div class="tabs">
    <div class="tab-nav">
      <div
        ref="tab-nav-item"
        class="tab-nav-item"
        @click="handleChangeTabItem(item, index)"
        :class="activeItem.value == item.value && 'activeClass'"
        v-for="(item, index) in options"
        :key="item.value || index"
      >
        {{ item.label }}
      </div>
      <div class="tab-nav-bar" :style="barStyle"></div>
    </div>
    <template v-for="item in options">
      <slot :name="item.value" v-if="activeItem.value == item.value"> </slot>
    </template>
  </div>
</template>
<script>
export default {
  props: {
    title: { type: String, default: "" },
    options: { type: Array, default: () => {} },
  },
  data() {
    return {
      activeItem: "",
      activeKey: "", // activeName name is the tabpane component's name
      barStyle: {},
    }
  },
  computed: {
    tabPanes() {
      return this.$children.filter((item) => item.$options.name === "TabPane")
    },
  },
  mounted() {
    this.activeItem = this.activeItem || this.options[0]
    this.updateBarStyle()
    console.log(this.tabPanes, "看看tabPanes")
  },
  methods: {
    updateBarStyle(index = 0) {
      // need to calculate the width and the offset of the nav-bar
      let preActiveIndex =
        this.options.findIndex((i) => i.value == this.activeItem.value) || 0
      // when click the same item , return
      if (preActiveIndex == index && index !== 0) return
      let preEl = this.$refs["tab-nav-item"][preActiveIndex]
      let elArr = this.$refs["tab-nav-item"]
      let el = this.$refs["tab-nav-item"][index]
      let offsetLeft = elArr.slice(0, index).reduce((a, b) => {
        a += b.offsetWidth
        return a
      }, 0)
      this.barStyle = {
        width: `${+el.offsetWidth - 20}px`,
        transform: (index && `translate(${offsetLeft}px)`) || "none",
      }
    },
    handleChangeTabItem(item, index) {
      console.log(item, "1111111")
      this.updateBarStyle(index)
      this.activeItem = item
    },
  },
}
</script>
<style scoped>
.tab-nav {
  position: relative;
  white-space: nowrap;
  overflow: scroll;
  -ms-overflow-style: none;

  /* border-bottom: 1px solid #d9d9d9; */
}
.tab-nav::-webkit-scrollbar {
  width: 0px !important;
}
/* .tab-nav::after {
  content: "";
  position: absolute;
  height: 2px;
  width: calc(100% - 20px);
  left: -20px;
  bottom: 0px;
  right: 0;
  margin: auto;
  background-color: #d9d9d9;
  z-index: 1;
} */

.tab-nav-item {
  display: inline-block;
  box-sizing: border-box;
  height: 40px;
  line-height: 40px;
  padding-right: 20px;
  cursor: pointer;
}

.tab-nav-bar {
  position: absolute;
  left: 0px;
  height: 2px;
  width: 1px;
  bottom: 0px;
  background-color: #1890ff;
  z-index: 2;
  transition: all 0.3s;
}
.activeClass {
  color: #1890ff;
}
</style>
