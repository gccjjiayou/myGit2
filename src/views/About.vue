<template>
  <div class="about">
    <input-number v-model="value" :max="10" :min="0"></input-number>
  </div>
</template>

<script>
import inputNumber from "@/components/inputNumber"
export default {
  components: {
    'input-number': inputNumber,
  },
  data() {
    return {
      value: -1,
    }
  }
  
}
</script>

<style>

</style>

