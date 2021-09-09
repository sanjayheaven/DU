<!-- du-confirm 仅用于 this.$du-confirm -->
<!-- 提供属性 -->
<!-- title -->
<!-- message -->
<!-- onClose -->
<!-- onConfrim -->

<template>
  <du-dialog v-model="show" :title="title" @confirm="handleConfirm">
    {{ message }}
  </du-dialog>
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
