<template>
  <div class="card">
    <!-- header -->
    <div class="header" v-if="$slots.header || title || $slots.extra">
      <slot v-if="$slots.header" name="header"></slot>
      <div v-else class="headDefault">
        <div class="headerDefaultTitle">
          <slot name="title" v-if="$slots.title"></slot>
          <div v-else>{{ title }}</div>
        </div>
        <slot name="extra"></slot>
      </div>
    </div>

    <!-- content / default -->
    <div class="content">
      <slot v-if="$slots.content" name="content"></slot>
      <slot v-else></slot>
    </div>

    <!-- footer -->
    <div class="footer" v-if="$slots.footer">
      <slot name="footer"></slot>
    </div>
  </div>
</template>
<script>
export default {
  props: { title: { type: String, default: "" } },
}
</script>
<style scoped>
.card {
  width: 100%;
  background-color: white;
}
.card:hover {
  box-shadow: 0 2px 12px 0 rgb(0 0 0 / 10%);
}
.card .header {
  padding: 18px 20px;
  border-bottom: 1px solid #ebeef5;
}
.card .header .headDefault {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.card .header .headerDefaultTitle {
  font-weight: bold;
}

.card .content {
  /* height: max-content; */
  /* overflow-y: auto; */
  padding: 18px 20px;
}
.card .footer {
  padding: 18px 20px;
}
</style>
