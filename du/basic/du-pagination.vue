<template>
  <ul>
    <li
      :class="[current == 1 && 'inActiveClass']"
      @click="current > 1 && $emit('change', current - 1)"
    ></li>
    <li @click="clickPage(1)" :class="[1 == current && 'currentClass']">1</li>
    <li @click="clickPage(current - 5)" v-if="showPreMore" class="preMore"></li>
    <li
      @click="clickPage(item)"
      :class="[item == current && 'currentClass']"
      v-for="(item, index) in middleArrays"
      :key="item || index"
    >
      {{ item }}
    </li>
    <li
      @click="clickPage(current + 5)"
      v-if="showNextMore"
      class="nextMore"
    ></li>
    <li
      @click="clickPage(pageCount)"
      :class="[pageCount == current && 'currentClass']"
    >
      {{ pageCount }}
    </li>
    <li
      :class="[current == pageCount && 'inActiveClass']"
      @click="current < pageCount && $emit('change', current + 1)"
    ></li>
  </ul>
</template>
<script>
export default {
  model: { prop: "current", event: "change" },
  props: {
    current: { type: Number, default: 1 },
    total: { type: Number, default: 0 },
    pageSize: { type: Number, default: 10 },
  },
  computed: {
    pageCount() {
      return parseInt(this.total / this.pageSize)
    },
    showPreMore() {
      if (this.current - 1 > 3) return true
      return false
    },
    showNextMore() {
      if (this.pageCount - this.current > 3) return true
      return false
    },
    middleArrays() {
      this.current
      const halfPageCount = (this.pageCount - 1) / 2
      if (this.showPreMore && this.showNextMore) {
        return [
          this.current - 2,
          this.current - 1,
          this.current,
          this.current + 1,
          this.current + 2,
        ]
      } else if (this.showNextMore) {
        return [2, 3, 4, 5, 6]
      } else if (this.showPreMore) {
        return [
          this.pageCount - 5,
          this.pageCount - 4,
          this.pageCount - 3,
          this.pageCount - 2,
          this.pageCount - 1,
        ]
      }
      let res = [...Array.from({ length: this.pageCount }, (a, b) => b + 1)]
      console.log(res, 222)
      return res.slice(1, this.pageCount - 1)
    },
  },
  data() {
    return {}
  },
  methods: {
    clickPage(item) {
      console.log(item, "看看当前什么item")
      if (item < 1) {
        item = 1
      } else if (item > this.pageCount) {
        item = this.pageCount
      }
      this.$emit("change", item)
    },
  },
}
</script>
<style scoped>
ul {
  list-style: none;
  display: flex;
  gap: 5px;
  padding: 0px;
}
li {
  cursor: pointer;
  width: 30px;
  height: 30px;
  line-height: 30px;
  border: 1px solid #d9d9d9;
  background-color: white;
  text-align: center;
}
li:hover,
.currentClass {
  border-color: #1890ff;
}

ul li:first-child,
ul li:last-child {
  position: relative;
}

ul li:first-child::after,
ul li:last-child::after {
  position: absolute;
  content: "";
  height: 8px;
  width: 8px;
  border-top: 1px solid;
  border-right: 1px solid;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  margin: auto;
}

ul li:first-child::after {
  transform: rotate(-135deg);
}
ul li:last-child::after {
  transform: rotate(45deg);
}

ul .inActiveClass {
  border-color: #d9d9d9;
  cursor: not-allowed;
}
.inActiveClass::after {
  border-top: 1px solid #d9d9d9 !important;
  border-right: 1px solid #d9d9d9 !important;
}
/* not elegant to use !important */

ul .preMore,
ul .nextMore {
  border: none;
  background: none;
}
ul .preMore::after,
ul .nextMore::after {
  content: "...";
}
ul .preMore:hover::after {
  content: "-5";
  color: #1890ff;
}
ul .nextMore:hover::after {
  content: "+5";
  color: #1890ff;
}
</style>
