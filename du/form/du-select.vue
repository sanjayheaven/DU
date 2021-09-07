<template>
  <div class="select">
    <input
      class="du-input"
      :readonly="!searchable"
      @click="showOptions = !showOptions"
      @blur="handleBlur"
      v-model="selectLabel"
    />
    <ul v-show="showOptions">
      <li
        v-for="(item, index) in options"
        :key="item.value || index"
        :value="item.value"
        @click="$emit('change', item.value)"
        :class="[value == item.value && 'activeClass']"
      >
        {{ item.label }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  model: { prop: "value", event: "change" },
  props: {
    value: { type: String, default: "" },
    options: { type: Array, default: () => [] },
    searchable: { type: Boolean, default: false },
    placeholder: { type: String, default: "" },
    disabled: { type: Boolean, default: false },
  },
  computed: {
    selectLabel() {
      let item = this.options.find((i) => i.value == this.value) || {}
      return item.label
    },
  },
  data() {
    return {
      data: [],
      showOptions: false,
    }
  },
  methods: {
    handleBlur() {
      setTimeout(() => {
        this.showOptions = false
      }, 100)
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
}
.du-input:hover {
  border: 1px solid #1890ff;
}

.du-input-textarea {
  height: 60px;
}
.select {
  width: 200px;
  position: relative;
  transition: all 0.3s;
}
input:hover {
  cursor: pointer;
  position: relative;
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

  z-index: 100;
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
