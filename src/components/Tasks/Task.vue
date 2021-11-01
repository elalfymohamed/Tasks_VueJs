<template>
  <div
    @dblclick="onToggleReminder(task.id)"
    :class="[task.reminder ? 'reminder' : '', 'task']"
  >
    <h3>
      {{ task.text }}
      <span @click="onDeleteTask(task.id)">
        <i class="fas fa-times"></i>
      </span>
    </h3>
    <p>{{ task.day }}</p>
  </div>
</template>

<script>
export default {
  name: "Task",
  props: {
    task: Object,
  },
  methods: {
    onDeleteTask(id) {
      this.$emit("delete-task", id);
    },
    onToggleReminder(id) {
      this.$emit("toggle-reminder", id);
    },
  },
};
</script>

<style scoped>
.fas {
  color: red;
}
.task {
  background: #f4f4f4;
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
}
.task.reminder {
  border-left: 5px solid green;
}
.task h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>
