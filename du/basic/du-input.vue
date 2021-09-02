<template>
  <textarea
    v-if="type === 'textarea'"
    :readonly="readonly"
    :disabled="disabled"
    :placeholder="placeholder"
    :rows="rows"
    :value="value"
    @input="(e) => $emit('input', e.target.value)"
    @click="$emit('click')"
    @blur="$emit('blur')"
  />
  <input
    v-else
    :readonly="readonly"
    :disabled="disabled"
    :placeholder="placeholder"
    :value="value"
    :type="type"
    @input="(e) => $emit('input', e.target.value)"
    @click="$emit('click')"
    @blur="$emit('blur')"
  />
</template>

<script>
export default {
  props: {
    type: { type: String, default: "" },
    readonly: { type: Boolean, default: false },
    disabled: { type: Boolean, default: false },
    placeholder: { type: String, default: "" },
    rows: { type: Number, default: 20 },

    value: { type: String, default: "" },
  },
  methods: {},
}
</script>
<style scoped>
input,
textarea {
  box-sizing: border-box;
  width: 200px;
  height: 35px;
  line-height: 35px;
  padding: 0px 10px;
  border: 1px solid #d9d9d9;
  border-radius: 0; /*clear input border-radius*/
  outline: none; /*cleat the outline black border*/
}
/* only padding left when the type is number, coz the influence of the up&down icon */
input[type="number"] {
  padding: 0px;
  padding-left: 10px;
}

textarea {
  height: 60px;
  line-height: normal;
  padding: 10px;
}

input:focus,
input:hover,
textarea:hover,
textarea:focus {
  border: 1px solid #1890ff;
}
</style>
