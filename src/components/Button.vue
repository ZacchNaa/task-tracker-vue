<template>
  <button
    :style="{ backgroundColor: color }"
    :class="className"
  >
    {{ text }}
  </button>
</template>

<script>
export default {
  name: "Button",
  props:{
    text: String,
    color: String,
    eventHander: Function,
    className: String
  }
}
</script>

<style scoped>

</style>