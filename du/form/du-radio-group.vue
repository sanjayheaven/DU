<template>
  <div class="radio-group">
    <label v-for="(item, index) in options" :key="item.value || index">
      <div :class="[item.value == value && 'is-checked']"></div>
      <input
        hidden
        type="radio"
        :checked="item.value == value"
        @change="$emit('change', item.value)"
      />
      <span>{{ item.label }} </span>
    </label>
  </div>
</template>

<script>
export default {
  model: { prop: "value", event: "change" },
  props: {
    value: { type: String, default: "" },
    options: { type: Array, default: () => [] },
  },
  methods: {
    handleChange(item, index) {},
  },
}
</script>
<style scoped>
.radio-group {
  display: flex;
  align-items: center;
  gap: 10px;
  flex-wrap: wrap;
}
.radio-group label {
  cursor: pointer;
  position: relative;
  display: flex;
  align-items: center;
}

.radio-group div {
  width: 14px;
  height: 14px;
  border-radius: 50%;
  border: 1px solid #d9d9d9;
  margin-right: 5px;
  /*this is why not use before&after to realize radio */
  background-color: white;
}

.radio-group span::before {
  content: "";
  position: absolute;
  left: 4px;
  width: 8px;
  height: 8px;
  top: 0;
  bottom: 0;
  margin-top: auto;
  margin-bottom: auto;
  border-radius: 50%;
}
.radio-group input[type="radio"]:checked + span::before {
  background-color: #1890ff;
  color: #1890ff;
}
.radio-group .is-checked {
  border: 1px solid #1890ff;
}
</style>
