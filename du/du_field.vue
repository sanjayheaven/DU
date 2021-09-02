<template>
  <div class="field">
    <div v-if="title" class="title">
      <span style="color: red" v-if="required">*</span>
      {{ title }}
    </div>
    <du_input
      v-if="!$slots.default"
      :placeholder="placeholder"
      v-model="value"
      :disabled="disabled"
      @change="$emit('change', value)"
    />
    <slot></slot>
  </div>
</template>

<script>
export default {
  model: { prop: "value", event: "change" },
  props: {
    value: { type: String, default: "" },
    title: { type: String, default: "" },
    type: { type: String, default: "" },
    required: { type: Boolean, default: false },
    placeholder: { type: String, default: "" },
    readonly: { type: Boolean, default: false },
    disabled: { type: Boolean, default: false },
  },
}
</script>
<style scoped>
.field {
  display: flex;
  align-items: center;
  margin: 10px 0px;
}
.field .title {
  width: 80px;
  margin-right: 10px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
</style>
