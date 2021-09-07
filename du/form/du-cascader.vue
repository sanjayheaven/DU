<template>
  <div class="cascader" @click.stop="">
    <input
      class="du-input"
      :readonly="!searchable"
      @click="showOptions = !showOptions"
      :value="selectLabel"
    />
    <du-cascader-panel
      class="fisrt-cascader-panel"
      v-if="showOptions"
      :options="options"
      :value="value"
      @change="handleChangeFirst"
    >
    </du-cascader-panel>
  </div>
</template>

<script>
export default {
  model: { prop: "value", event: "change" },
  props: {
    value: { type: Array, default: () => [] },
    options: { type: Array, default: () => [] },
  },
  mounted() {
    document.body.addEventListener("click", () => {
      this.showOptions = false
    })
  },
  computed: {
    selectLabel() {
      // according to the value find the label
      let options = this.options
      return this.value
        .reduce((acc, item, index, arr) => {
          let existItem = options.find((option) => option.value == item) || {}
          options = existItem.children || []
          acc.push(existItem.label)
          return acc
        }, [])
        .join(" / ")
    },
  },
  data() {
    return {
      showOptions: false,
    }
  },
  methods: {
    handleChangeFirst(value) {
      console.log("这是第一个", value)
      this.$emit("change", value)
      this.showOptions = false
    },
    handleClickLi(item) {
      console.log(item, item.children)
    },
  },
}
</script>
<style scoped>
.du-input {
  box-sizing: border-box;
  width: 200px;
  height: 35px;
  line-height: 35px;
  padding: 0px 10px;
  border: 1px solid #d9d9d9;
  border-radius: 0px; /*clear input border-radius*/
  outline: none; /*cleat the outline black border*/

  white-space: nowrap;
  text-overflow: ellipsis;
  overflow: hidden;
}
.du-input:hover {
  border: 1px solid #1890ff;
}

.cascader {
  width: 200px;
  position: relative;
  transition: all 0.3s;
  z-index: 10001;
}
input:hover {
  cursor: pointer;
  position: relative;
}

.select input:after {
  /*三角箭头*/
  position: absolute;
  top: 10px;
  right: 10px;
  width: 0px;
  height: 0px;
  content: "666676876786";
  border: 6px solid transparent;
  border-top-color: black;
}
</style>
