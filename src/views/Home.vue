<template>
  <AddTask v-show="showAddTask" @add-task="addTask" />

  <Tasks
    @toggle-reminder="toggleReminder"
    @delete-task="deleteTask"
    :tasks="tasks"
  />
</template>

<script>
import AddTask from "../components/Tasks/AddTask.vue";
import Tasks from "../components/Tasks/Tasks.vue";
export default {
  name: "Home",
  props: {
    showAddTask: Boolean,
  },
  components: {
    AddTask,
    Tasks,
  },
  data() {
    return {
      tasks: [],
    };
  },
  methods: {
    // add task
    async addTask(task) {
      const res = await fetch(`api/tasks`, {
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
    async deleteTask(id) {
      const res = await fetch(`api/tasks/${id}`, {
        method: "DELETE",
      });
      res.status === 200
        ? (this.tasks = this.tasks.filter((t) => t.id !== id))
        : alert("Error deleting task");
    },
    // Toggle Reminder ()
    async toggleReminder(id) {
      const taskToToggle = await this.fetchDataTask(id);
      const updTask = { ...taskToToggle, reminder: !taskToToggle.reminder };
      const res = await fetch(`api/tasks/${id}`, {
        method: "PUT",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(updTask),
      });
      const data = await res.json();
      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, reminder: data.reminder } : task
      );
    },
    // fetch data in json
    async fetchDataTasks() {
      const res = await fetch(`api/tasks`);
      const data = await res.json();
      return data;
    },
    async fetchDataTask(id) {
      const res = await fetch(`api/tasks/${id}`);
      const data = await res.json();
      return data;
    },
  },

  async created() {
    this.tasks = await this.fetchDataTasks();
  },
};
</script>
