<template>
  <div class="progress">
    <div class="progress-bg">
      <div class="progress-bar" :style="barStyle"></div>
    </div>
    <div>{{ value }}%</div>
  </div>
</template>
<script>
export default {
  computed: {
    barStyle() {
      return {
        width: this.value + "%",
      }
    },
  },
  props: {
    value: { type: Number, default: 0, required: true },
  },
  data() {
    return {}
  },
}
</script>
<style scoped>
.progress {
  display: flex;
  align-items: center;
  gap: 5px;
}
.progress-bg {
  width: 200px;
  height: 10px;
  background-color: #d9d9d9;
  border-radius: 20px;
}
.progress-bar {
  width: 100px;
  min-width: 0%;
  max-width: 100%;
  height: 100%;
  background-color: #1890ff;
  border-radius: 20px;
  transition: all 0.3s;
}
</style>
