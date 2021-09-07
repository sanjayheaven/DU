<template>
  <label class="switch">
    <input
      hidden
      type="checkbox"
      :checked="value"
      @change="(e) => $emit('change', e.target.checked)"
    />
    <div></div>
  </label>
</template>

<script>
export default {
  model: { prop: "value", event: "change" },
  props: {
    value: { type: Boolean, default: false },
    disabled: { type: Boolean, default: false },
  },
}
</script>
<style scoped>
.switch div {
  cursor: pointer;
  position: relative;
  width: 48px;
  height: 24px;
  border-radius: 20px; /*larger than half of the height */
  background: #bfbfbf;
  transition: all 0.3s ease;
}
.switch div:after {
  content: "";
  position: absolute;
  top: 0;
  bottom: 0;
  margin-top: auto;
  margin-bottom: auto;
  left: 2px;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background-color: white;
  transition: all 0.3s ease;
}
.switch input:checked + div {
  background-color: #1890ff;
}
.switch input:checked + div:after {
  transform: translateX(24px);
}
</style>
