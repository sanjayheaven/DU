<template>
  <div v-if="show" class="dialog" @click="close">
    <div
      class="modal"
      @click.stop=""
      :class="[closeAnimate ? 'modal-scale ' : '']"
    >
      <!-- 关闭符号 -->
      <i
        @click="close"
        style="position: absolute;top:10px;right: 10px;cursor: pointer;"
        class="u1__close"
      ></i>

      <!-- header -->
      <div class="header" v-if="$slots.header || $slots.title || title">
        <slot v-if="$slots.header" name="header"></slot>
        <div class="headerDefault">
          <slot name="title" v-if="$slots.title"></slot>
          <div v-else>{{ title }}</div>
        </div>
      </div>

      <!-- content / default -->
      <div class="content">
        <slot v-if="$slots.content" name="content"></slot>
        <slot v-else></slot>
      </div>

      <!-- footer  -->
      <div class="footer" v-if="showFooter">
        <slot v-if="$slots.footer" name="footer"></slot>
        <div class="footerDefault" v-else>
          <du-button @click="close" style="margin-right: 20px;">
            {{ (isEn && "Cancel") || "取消" }}
          </du-button>
          <du-button @click="$emit('confirm')" type="primary">
            {{ (isEn && "Confirm") || "确定" }}
          </du-button>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  model: { prop: "show", event: "change" },
  props: {
    show: { type: Boolean, default: false },
    title: { type: String, default: "" },
    showFooter: { type: Boolean, default: true }, // 是否显示底部区域
  },
  data() {
    return { timer: null, closeAnimate: false }
  },
  methods: {
    close() {
      this.closeAnimate = true
      this.timer = setTimeout(() => {
        this.timer = null
        this.closeAnimate = false
        this.$emit("change", false)
        this.$emit("close")
      }, 300)
    },
  },
}
</script>
<style scoped>
.dialog {
  position: fixed;
  z-index: 10001;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: rgb(118, 118, 118, 0.45);
}

.dialog .modal {
  min-width: 40%;
  width: max-content;
  background-color: white;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  opacity: none;
  animation: zoomIn;
  animation-duration: 0.3s;
  position: relative;
}
@keyframes zoomIn {
  from {
    opacity: 0;
    transform: scale3d(0.3, 0.3, 0.3);
  }
  50% {
    opacity: 1;
  }
}
.dialog .modal-scale {
  transform: scale(0);
  transition: all 0.3s ease-out;
}
.dialog .modal .header {
  padding: 15px 20px;
  border-bottom: 1px solid #d9d9d9;
}
.dialog .modal .headerDefault {
  display: flex;
  align-items: center;
  justify-content: space-between;
  font-weight: bold;
}
.dialog .modal .content {
  width: max-content;
  overflow-y: auto;
  padding: 25px 20px;
  margin: auto;
}
.dialog .modal .footer {
  padding: 15px 20px;
}
.dialog .modal .footerDefault {
  display: flex;
  align-items: center;
  padding: 0px 20px;
  justify-content: center;
}
</style>
