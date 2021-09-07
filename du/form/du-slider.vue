<template>
  <div class="slider" style="width: 200px;">
    <div class="slider-thumb"></div>
  </div>
</template>

<script>
export default {
  props: {
    type: { type: String, default: "default" },
    disabled: { type: Boolean, default: false },
    label: { type: String, default: "" },
  },
  data() {
    return {}
  },
}
</script>
<style scoped>
.slider {
  width: 200px;
  height: 10px;
  background-color: #1890ff;
  border-radius: 20px;
  position: relative;

  
  cursor: pointer;

}
.slider-thumb {
  width: 20px;
  height: 20px;
  background-color: white;
  border-radius: 50%;
  position: absolute;
  top: 0px;
  bottom: 0px;
  margin-top: auto;
  margin-bottom: auto;

  border: 1px solid #d9d9d9;
  cursor: pointer;
}
</style>
