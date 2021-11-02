<template>
  <div
    @dblclick="onToggleReminder(task.id)"
    :class="[task.reminder ? 'reminder' : '', 'task']"
  >
    <h3>
      {{ task.text }}
      <span
        @click="
          onDeleteTaskDI(task.id);
          isShowMassege();
        "
      >
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
    onDeleteTaskDI(id) {
      this.$emit("delete-taskDI", id);
    },
    onToggleReminder(id) {
      this.$emit("toggle-reminder", id);
    },
    isShowMassege() {
      this.$emit("isShow-massage-task");
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
