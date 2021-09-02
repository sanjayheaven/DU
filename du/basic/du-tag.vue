<template>
  <span
    class="tag"
    :style="{ 'background-color': color, color: color && 'white' }"
  >
    <slot></slot>
    <span @click="$emit('close')" class="close"> </span>
  </span>
</template>

<script>
export default {
  props: {
    closable: { type: Boolean, default: false },
    color: { type: String, default: "" },
  },
}
</script>
<style scoped>
.tag {
  padding: 2px 10px;
  border: 1px solid #d9d9dd;
  font-size: smaller;
}

.tag .close {
  margin: 0px 10px;
  position: relative;
  cursor: pointer;
}

.tag .close::before,
.tag .close::after {
  content: "";
  width: 2px;
  height: 12px;
  background-color: currentColor;
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  margin: auto;
}
.close::before {
  transform: rotate(45deg);
}

.close::after {
  transform: rotate(-45deg);
}
</style>
