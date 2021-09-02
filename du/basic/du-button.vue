<template>
  <button
    @click="$emit('click')"
    style="cursor: pointer"
    :disabled="disabled"
    :style="buttonClass[type]"
  >
    <span v-if="label">{{ label }}</span>
    <slot v-else></slot>
  </button>
</template>

<script>
export default {
  props: {
    type: { type: String, default: "default" },
    disabled: { type: Boolean, default: false },
    label: { type: String, default: "" },
  },
  data() {
    return {
      buttonClass: {
        default: { "background-color": "white", border: "1px solid #d9d9d9" },
        primary: { "background-color": "#1890ff", color: "white" },
        danger: { "background-color": "#ff4d4f", color: "white" },
      },
    }
  },
}
</script>
<style scoped>
button {
  height: 32px;
  padding: 0px 15px;
  transition: all 0.3s;
  border: none;
}
button:hover {
  opacity: 0.7;
}
</style>
