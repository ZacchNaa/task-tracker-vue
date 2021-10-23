<template>
  <AddTask v-if="showAddTaskForm" @ADD_NEW_TASK="addTaskHandler" />
    <Tasks
      @toggle-reminder="toggleReminderHandler"
      @delete-task="deleteTaskHandler"
      :tasks="tasks"
    />
</template>

<script>
import AddTask from "../components/AddTask.vue";
import Tasks from "../components/Tasks.vue";
export default {
    name:'Home',
    props:{
        showAddTaskForm: Boolean
    },
    components: {AddTask, Tasks},
    data() {
    return {
      tasks: [],
    };
  },
  methods: {
    // add new task
    async addTaskHandler(task) {
      const res = await fetch("api/tasks", {
        method: "POST",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(task),
      });

      const data = await res.json();
      this.tasks = [...this.tasks, data];
    },
    // delete task
    async deleteTaskHandler(id) {
      if (confirm("Are you sure you want delete this item?")) {
        const res = await fetch(`api/tasks/${id}`, { method: "DELETE" });

        res.status === 200
          ? (this.tasks = this.tasks.filter((task) => task.id !== id))
          : alert("Error deleting task");
      }
    },
    // toggle reminder
    async toggleReminderHandler(id) {
      // Method 1
      // this.tasks[id-1].reminder = !this.tasks[id-1].reminder
      // Method 2
      const taskToToggle = await this.fetchTask(id) //fetch the toggled task
      // update the task reminder
      const updatedTask = {...taskToToggle, reminder: !taskToToggle.reminder}
      // send the update request
      const res = await fetch(`api/tasks/${id}`, {
        method: 'PUT',
        headers: {
          'Content-type': 'application/json'
        },
        body: JSON.stringify(updatedTask)
      })

      // get the json data
      const data = await res.json()
      // update the tasks array
      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, reminder: data.reminder } : task
      );
    },

    // fetch all data from the backend
    async fetchTasks() {
      const res = await fetch("api/tasks");
      const data = await res.json();

      return data;
    },

    // fetch single data from the backend
    async fetchTask(id) {
      const res = await fetch(`api/tasks/${id}`);
      const data = await res.json();

      return data;
    },
  },
  async created() {
    this.tasks = await this.fetchTasks();    
  },

}
</script>

<style>

</style>