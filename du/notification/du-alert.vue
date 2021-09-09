<template>
  <du-dialog v-model="show" :title="title">
    <div
      style="
        max-width: 40vw;
        line-height: 30px;
        word-break: break-word;
        text-align: center;
        font-size: larger;
        font-weight: bold;
        color: red;
      "
    >
      {{ message }}
    </div>
    <div slot="footer" style="display: flex; justify-content: center">
      <div
        @click="show = false"
        class="du-_button"
        style="background: linear-gradient(180deg, #31c6fc 0%, #40a4fa 100%)"
      >
        Close
        <!-- {{ (isEn && "Close") || "关闭" }} -->
      </div>
    </div>
  </du-dialog>
</template>
<script>
export default {
  components: {},
  created() {},
  data() {
    return {
      show: false,
      title: "",
      message: "",
    }
  },
}
</script>
<style scoped></style>
