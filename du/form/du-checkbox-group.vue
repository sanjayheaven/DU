<template>
  <div class="checkbox-group">
    <label v-for="(item, index) in options" :key="item.value || index">
      <div :class="[value.includes(item.value) && 'is-checked']"></div>
      <input
        hidden
        type="checkbox"
        :checked="value.includes(item.value)"
        @click="handleChange(item, index)"
      />
      <span>{{ item.label }} </span>
    </label>
  </div>
</template>

<script>
export default {
  model: { prop: "value", event: "change" },
  props: {
    value: { type: Array, default: () => [] },
    options: { type: Array, default: () => [] },
  },
  methods: {
    handleChange(item, index) {
      let existIndex = this.value.indexOf(item.value)
      if (existIndex != -1) {
        this.value.splice(existIndex, 1)
      } else {
        this.value.push(item.value)
      }
      this.$emit("change", this.value)
    },
  },
}
</script>
<style scoped>
/* similar style to radio-group */
.checkbox-group {
  display: flex;
  align-items: center;
  gap: 10px;
  flex-wrap: wrap;
}
.checkbox-group label {
  cursor: pointer;
  position: relative;
  display: flex;
  align-items: center;
}

.checkbox-group div {
  width: 14px;
  height: 14px;
  border: 1px solid #d9d9d9;
  margin-right: 5px;
  /*this is why not use before&after to realize checkbox */
  background-color: white;
}

.checkbox-group span::before {
  content: "";
  position: absolute;
  left: 4px;
  width: 4px;
  height: 8px;
  top: 0;
  bottom: 0;
  margin-top: auto;
  margin-bottom: auto;
}
.checkbox-group input[type="checkbox"]:checked + span::before {
  border-right: 2px solid white;
  border-bottom: 2px solid white;
  transform: rotate(45deg);
}
.checkbox-group .is-checked {
  border: 1px solid #1890ff;
  background-color: #1890ff;
}
</style>
