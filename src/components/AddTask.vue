<template>
  <form @submit.prevent="formSubmitHandler" class="add-form">
    <div class="form-control">
      <label>Task</label>
      <input v-model="text" type="text" name="text" placeholder="Add Task" />
    </div>
    <div class="form-control">
      <label>Day & Time</label>
      <input v-model="day" type="text" name="day" placeholder="Add Day & Time" />
    </div>
    <div class="form-control form-control-check">
      <label>Set Reminder</label>
      <input v-model="reminder" type="checkbox" name="reminder" />
    </div>
    <Button className="btn btn-block" text="Save Task" />
    <!-- <input type="submit" value class="" /> -->
  </form>
</template>

<script>
import Button from "./Button.vue";
export default {
  name: "AddTask",
  components: { Button },
  data() {
    return {
      text: "",
      day: "",
      reminder: false,
    };
  },

  methods:{
    formSubmitHandler() {
        if (!this.text || !this.day) {
            alert('Please provide both task and day')
            return
        }

        const newTask = {
            // id: Math.floor(Math.random() * 100000),
            text: this.text,
            day: this.day,
            reminder: this.reminder
        }

        // console.log(newTask);
        // emit newTask object up
        this.$emit('ADD_NEW_TASK', newTask)

        // clear inputs after submission
        this.text = ''
        this.day = ''
        this.reminder = false
        // console.log(`${this.text} - ${this.day}`);
    }
  }
};
</script>

<style>
.add-form {
  margin-bottom: 40px;
}
.form-control {
  margin: 20px 0;
}
.form-control label {
  display: block;
}
.form-control input {
  width: 100%;
  height: 40px;
  margin: 5px;
  padding: 3px 7px;
  font-size: 17px;
  border: 0.5px solid #f1f1f1;
  border-radius: 5px;
  background-color: #f6f6f6;
  outline: none;
}
.form-control-check {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.form-control-check label {
  flex: 1;
}
.form-control-check input {
  flex: 2;
  height: 20px;
}
</style>