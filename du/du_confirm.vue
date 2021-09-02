<!-- u1_confirm 仅用于 this.$u1_confirm -->
<!-- 提供属性 -->
<!-- title -->
<!-- message -->
<!-- onClose -->
<!-- onConfrim -->

<template>
  <u1_dialog v-model="show" :title="title" @confirm="handleConfirm">
    {{ message }}
  </u1_dialog>
</template>
<script>
export default {
  props: {},
  components: {},
  created() {},
  data() {
    return {
      show: false,
      title: "Confirm",
      message: "",
      onClose: null,
      onConfirm: null,
    }
  },
  methods: {
    handleClose() {
      this.show = false
      this.onClose && this.onClose()
    },
    handleConfirm() {
      this.show = false
      this.onConfirm && this.onConfirm()
    },
  },
}
</script>
<style scoped></style>
