<template>
  <header>
    <h1>{{ title }}</h1>
    <Button v-show="isHomePage" @click="$emit('TOGGLE_ADD_TASK_FORM')" :text="!toggleAddTaskBtn? 'Add Task': 'Close'" :color="toggleAddTaskBtn? 'red': 'green'" className="btn" />
  </header>
</template>
// *************************SCRIPTS*****************************
<script>
import Button from "./Button.vue";
export default {
  name: "Header",
  props: { title: String, toggleAddTaskBtn:Boolean },
  components: { Button },
  computed: {
    // deciding where to show header button
    isHomePage() {
      if (this.$route.path==="/") {
        return true
      } else {
        return false
      }
    }
  }
};
</script>

// *************************STYLES*****************************
<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
</style>

