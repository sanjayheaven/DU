<template>
  <div>
    <table>
      <thead>
        <tr>
          <th v-if="draggable"></th>
          <th v-if="showNo">No.</th>
          <th v-for="(item, index) in columns" :key="item.value || index">
            {{ item.label }}
          </th>
        </tr>
      </thead>
      <draggable :list="data" tag="tbody" handle=".handle">
        <tr v-for="(item, index) in data" :key="item._id || index">
          <td v-if="draggable" class="handle">
            <i class="el-icon-s-operation"></i>
          </td>
          <td v-if="showNo">{{ index + 1 }}</td>
          <td v-for="(col, colIndex) in columns" :key="col._id || colIndex">
            <slot
              v-if="$slots[col.value] || $scopedSlots[col.value]"
              :name="col.value"
              :text="item[col.value]"
              :record="item"
              :index="index"
            ></slot>
            <div v-else>{{ item[col.value] }}</div>
          </td>
        </tr>
      </draggable>
    </table>
    <div style="display: flex;flex-direction: row-reverse;">
      <du-pagination
        v-model="pagination.current"
        :total="total"
      ></du-pagination>
    </div>
    <div
      v-if="!data.length"
      style="
          border-bottom-left-radius: 5px;
          border-bottom-right-radius: 5px;
          width: 100%;background-color: white;padding: 40px 0px;text-align: center;"
    >
      Empty !
    </div>
  </div>
</template>
<script>
import draggable from "vuedraggable"
export default {
  components: { draggable },
  props: {
    draggable: { type: Boolean, default: false },
    showNo: { type: Boolean, default: false },
    columns: { type: Array, default: () => [] },
    data: { type: Array, default: () => [] },
    pagination: { type: Object, default: () => {} },
  },
  computed: {
    total() {
      return this.data.length
    },
  },
  data: () => {
    return {
      current: "1",
    }
  },
}
</script>
<style scoped>
table {
  width: 100%;
  border-collapse: separate;
  border-spacing: 0;
}
tr {
  background-color: white;
}
thead {
  width: 100%;
}
thead tr {
  /* background-color: #f2f2f2; */
  background-color: #fafafa;
}
th {
  padding: 18px 12px;
  min-width: max-content;
  border-bottom: 1px solid #d9d9d9;
  text-align: left;
}
tbody tr:hover {
  background-color: #e6f7ff;
}
td {
  padding: 10px;
  border-bottom: 1px solid #d9d9d9;
}
</style>
