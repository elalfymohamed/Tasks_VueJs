<template>
  <AddTask
    v-show="showAddTask"
    @add-task="addTask"
    @isShow-massage-addTask="isShowMassageAT"
  />
  <div class="loading" v-if="loading">
    <p>Loading....</p>
  </div>
  <div class="tasks-empty" v-if="tasks.length ? false : true && !loading">
    <div class="empty">
      <p>Tasks are empty</p>
    </div>
  </div>
  <Tasks
    @toggle-reminder="toggleReminder"
    @delete-taskDI="deleteTaskDI"
    @isShow-massage-task="isShowMassageDT"
    :tasks="tasks"
  />
  <MDelete
    @isShow-massage-task="isShowMassageDT"
    @delete-task="deleteTask"
    :isShowMessageTask="isShowMessageTask"
    :isShowMessageAddTask="isShowMessageAddTask"
  />
</template>

<script>
import AddTask from "../components/Tasks/AddTask.vue";
import Tasks from "../components/Tasks/Tasks.vue";
import MDelete from "../components/Massage/MDelete.vue";
export default {
  name: "Home",
  props: {
    showAddTask: Boolean,
  },

  components: {
    AddTask,
    Tasks,
    MDelete,
  },
  data() {
    return {
      tasks: [],
      loading: false,
      isShowMessageTask: false,
      isShowMessageAddTask: false,
      taskID: "",
    };
  },
  methods: {
    //  show massage delete task
    isShowMassageDT() {
      this.isShowMessageTask = !this.isShowMessageTask;
    },
    // show massage add task
    isShowMassageAT() {
      this.isShowMessageAddTask = !this.isShowMessageAddTask;

      if (this.isShowMessageAddTask) {
        setTimeout(() => {
          this.isShowMessageAddTask = false;
        }, 2000);
      }
    },
    // set task id to delete a task in MDelete component and show massage
    deleteTaskDI(id) {
      this.taskID = id;
    },
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
    async deleteTask() {
      const DI = this.taskID;
      const res = await fetch(`api/tasks/${DI}`, {
        method: "DELETE",
      });
      res.status === 200
        ? (this.tasks = this.tasks.filter((t) => t.id !== DI))
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
      this.loading = true;
      const res = await fetch(`api/tasks`);
      const data = await res.json();
      this.loading = false;
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

<style scoped>
.loading {
  text-align: center;
  margin: 90px 0;
}

.tasks-empty .empty {
  text-align: center;
  margin: 90px 0;
}
.empty p {
  font-size: 20px;
  color: rgba(0, 0, 0, 0.575);
}
</style>
