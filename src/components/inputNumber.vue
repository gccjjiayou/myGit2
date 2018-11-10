<template>
  <div class="input-number">
    <el-input type="text" :value="currentValue" @change="handleChange"></el-input>{{this.currentValue}}
    <el-button type="primary" @click="handleUp" :disabled="currentValue >= max">+1</el-button>
    <el-button type="primary" @click="handleDown" :disabled="currentValue <= min">-1</el-button>
  </div>
</template>
<script>
function isValueNumber(val) {
    return (/(^-?[0-9]+\.{1}\d+$) | (^-?[1-9][0-9]*$) | (^-?0{1}$)/).test(val + "")
  }
</script>

<script>
export default {
  
  props: {
    max: {
      type: Number,
      default: Infinity
    },
    min: {
      type: Number,
      default: -Infinity
    },
    value: {
      type: Number,
      default: 0
    }
  },
  data() {
    return {
      currentValue: this.value
    };
  },
  watch: {
    currentValue(val) {
      this.$emit("input", val);
      this.$emit("on-change", val);
    },
    value(val) {
      this.updateValue(val);
    }
  },
  methods: {
    updateValue(val) {
      this.currentValue =
        val > this.max ? this.max : val < this.min ? this.min : val;
    },

    handleChange(event) {
      var val = event.target.value.trim();
      var max = this.max;
      var min = this.min;
      var isNumber = (/(^-?[0-9]+\.{1}\d+$) | (^-?[1-9][0-9]*$) | (^-?0{1}$)/).test(val + "")
      if (isNumber) {
        // val = Number(val);
        this.currentValue = val;
        if (val > max) {
          this.currentValue = val;
        } else if (val < min) {
          this.currentValue = val;
        } else {
          event.target.value = this.currentValue;
        }
      }
    },
    handleUp() {
      if (this.currentValue >= this.max) return;
      this.currentValue += 1;
    },
    handleDown() {
      if (this.currentValue <= this.min) return;
      this.currentValue -= 1;
    }
  },
  mounted() {
    this.updateValue(this.value);
  }
};
</script>

<style>
</style>
