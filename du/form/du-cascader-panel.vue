<template>
  <div class="cascader-panel">
    <ul>
      <li
        v-for="(item, index) in options"
        :key="item.value || index"
        :value="item.value"
        @click.stop="handleClick(item, index)"
        :class="[activeChild.value == item.value && 'activeClass']"
      >
        {{ item.label }}
        <i v-if="item.children && item.children.length" class="right-arrow"></i>
      </li>
    </ul>
    <du-cascader-panel
      :value="value.slice(1)"
      @change="(value) => $emit('change', [activeChild.value, ...value])"
      class="cascader-panel-child"
      v-if="activeChild.children && activeChild.children.length"
      :options="childrenOptions"
    >
    </du-cascader-panel>
  </div>
</template>

<script>
export default {
  name: "cascader-panel",
  model: { prop: "value", event: "change" },
  mounted() {
    this.activeChild = this.options.find((i) => i.value == this.value[0]) || {}
  },
  computed: {
    childrenOptions() {
      return this.activeChild.children || []
    },
  },
  props: {
    value: { type: Array, default: () => [] },
    options: { type: Array, default: () => [] },
  },
  data() {
    return {
      activeChild: {},
      selectLabel: "",
    }
  },
  methods: {
    handleOnLevel(level) {
      console.log(level, 222)
      this.$emit("change", [this.activeChild.value, ...level])
    },
    handleClick(item, index) {
      this.activeChild = {}
      this.$nextTick(() => {
        this.activeChild = JSON.parse(JSON.stringify(item))
        // to click the item that has expand the more then 2 level child , only show the 1 level child
      })
      if (!item.children || !item.children.length) {
        this.$emit("change", [item.value])
      }
    },
  },
}
</script>
<style scoped>
.cascader-panel {
  width: 200px;
  position: relative;
  transition: all 0.3s;
  z-index: 10001;
}
.cascader-panel-child {
  position: absolute;
  top: 0px;
  left: 100%;
  background-color: black;
}
.activeClass {
  background-color: #e6f7ff;
}
ul {
  position: absolute;
  box-sizing: border-box;
  background-color: white;
  width: 100%;
  padding: 0px;
  margin-top: 2px;
  list-style: none;
  box-shadow: 0 2px 12px 0 rgb(0 0 0 / 10%);

  max-height: calc(35 * 5px); /*max show 5 li*/
  overflow-y: scroll;

  z-index: 10001;
}

ul li {
  height: 35px;
  line-height: 35px;
  padding: 0px 10px;
}
ul li:hover {
  cursor: pointer;
  background-color: #e6f7ff;
}

li {
  position: relative;
}
i {
  top: 0;
  bottom: 0;
  margin-top: auto;
  margin-bottom: auto;
  right: 5px;
  transform: scale(0.5);
}
.right-arrow {
  position: absolute;
  width: 16px;
  height: 16px;
  border-right: 1px solid currentColor;
  border-bottom: 1px solid currentColor;
  transform: scale(0.5) rotate(-45deg);
}
</style>
