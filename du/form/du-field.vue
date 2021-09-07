<template>
  <div class="field">
    <!-- if element overflows then show tooltip -->
    <div v-if="title">
      <du-tooltip :label="title" v-if="showTooltip">
        <div class="title">
          <span style="color: red" v-if="required">*</span>
          {{ title }}
        </div>
      </du-tooltip>

      <div v-else class="title" ref="title">
        <span style="color: red" v-if="required">*</span>
        {{ title }}
      </div>
    </div>

    <du_input
      v-if="!$slots.default"
      :placeholder="placeholder"
      :type="type"
      v-model="value"
      :disabled="disabled"
      @input="$emit('change', value)"
    />
    <slot></slot>
  </div>
</template>

<script>
export default {
  mounted() {
    let el = this.$refs.title
    console.log("看看元素", el.scrollWidth, el.clientWidth)
    if (el.scrollWidth > el.clientWidth) {
      this.showTooltip = true
    }
    // console.log(this.$refs.title, "看看title元素的宽度是否溢出")
  },
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
  data() {
    return { showTooltip: false }
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
