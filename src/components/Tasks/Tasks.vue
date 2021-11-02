<template>
  <div :key="task.id" v-for="task in tasks" class="contenr-task">
    <Task
      @toggle-reminder="$emit('toggle-reminder', task.id)"
      @delete-taskDI="$emit('delete-taskDI', task.id)"
      :task="task"
      @isShow-massage-task="$emit('isShow-massage-task')"
    />
  </div>
</template>

<script>
import Task from "./Task.vue";
export default {
  name: "Tasks",
  props: {
    tasks: Array,
  },
  components: {
    Task,
  },
  emits: ["delete-taskDI", "toggle-reminder", "isShow-massage-task"],
};
</script>
