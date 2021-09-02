<template>
  <div style="background-color: white;">
    <div style="font-size: larger;font-weight: bold;">
      <div style="display: flex;">
        <div class="col">
          <div class="keyItem" @click="handleChange('7')">7</div>
          <div class="keyItem" @click="handleChange('4')">4</div>
          <div class="keyItem" @click="handleChange('1')">1</div>
          <div class="keyItem" @click="handleChange('00')">00</div>
        </div>
        <div class="col">
          <div class="keyItem" @click="handleChange('8')">8</div>
          <div class="keyItem" @click="handleChange('5')">5</div>
          <div class="keyItem" @click="handleChange('2')">2</div>
          <div class="keyItem" @click="handleChange('0')">0</div>
        </div>
        <div class="col">
          <div class="keyItem" @click="handleChange('9')">9</div>
          <div class="keyItem" @click="handleChange('6')">6</div>
          <div class="keyItem" @click="handleChange('3')">3</div>
          <div class="keyItem" @click="handleChange('.')">.</div>
        </div>
        <div class="col" style="color: red;" v-if="showAmount">
          <div class="keyItem" @click="handleAmount('100')">S$100</div>
          <div class="keyItem" @click="handleAmount('50')">S$50</div>
          <div class="keyItem" @click="handleAmount('20')">S$20</div>
          <div class="keyItem" @click="handleAmount('10')">S$10</div>
        </div>
        <div class="col">
          <div class="keyItem" @click="handleBack">
            {{ (isEn && "Del") || "撤退" }}
          </div>
          <div class="keyItem" @click="handleClear">
            {{ (isEn && "AC") || "清除" }}
          </div>
          <div v-if="showCancel" class="keyItem" @click="$emit('cancel')">
            {{ (isEn && "Cancel") || "取消" }}
          </div>
          <div v-if="showCancel" class="keyItem" @click="$emit('confirm')">
            {{ (isEn && "Confirm") || "确定" }}
          </div>
          <div
            v-else
            class="keyItem"
            style="height: 130px;background-color:#FFA821;"
            @click="$emit('confirm', value)"
          >
            {{ (isEn && "Confirm") || "确定" }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  computed: {
    isEn() {
      return (
        (this.$store && this.$store.state.isEn) ||
        localStorage.getItem("isEn") == "en"
      )
    },
  },
  model: { prop: "value", event: "change" },
  props: {
    value: { type: String, default: "" },
    show: { type: Boolean, default: false },
    showCancel: { type: Boolean, default: false }, // 显示取消按钮
    showAmount: { type: Boolean, default: false }, // 显示金额那一列
    title: { type: String, default: "" },
  },

  data() {
    return {
      clickAmount: false,
    }
  },
  methods: {
    handleAmount(item) {
      this.clickAmount = true
      this.$emit("change", item)
    },
    handleChange(item) {
      // 清空快捷选项
      if (this.clickAmount) {
        this.value = ""
        this.clickAmount = false
      }

      if (item == ".") {
        this.value = this.value + item
        this.value = (+this.value || 0) + "."
        this.$emit("change", this.value)
        return
      }
      if (item == "0") {
        console.log(this.value, 33333333333333)
        this.value = (+this.value || "") + "0"
        console.log(this.value, 55555555555555)
        this.$emit("change", this.value)
        return
      }
      if (!this.value[this.value.length - 1] === ".") {
        this.value = (+this.value || 0) + item
      } else {
        this.value = this.value + item
      }

      this.$emit("change", +this.value + "")
    },
    handleBack() {
      console.log(this.value, typeof this.value)
      this.value = this.value.slice(0, -1)
      if (!this.value.length) {
        this.$emit("change", "")
        return
      }
      this.$emit("change", +this.value + "")
      this.$emit("back")
    },
    handleClear() {
      this.value = ""
      this.$emit("change", "")
      this.$emit("clear", "")
    },
  },
}
</script>
<style scoped>
.keyItem {
  padding: 15px;
  margin: 3px 5px;
  width: 3rem;
  height: 3rem;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  border: 1px solid gray;
  border-radius: 5px;
  border: 1px solid #d6d6d6;
}
.keyItem:active {
  border: 1px solid #fa8400;
}
.col:first-child div {
  margin-left: 0;
}
.col:last-child div {
  margin-right: 0;
}
.col :first-child {
  margin-top: 0;
}
.col :last-child {
  margin-bottom: 0;
}
</style>
