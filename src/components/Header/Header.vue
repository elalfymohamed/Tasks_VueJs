<template>
  <header class="header">
    <div>
      <h1>{{ title }}</h1>
    </div>
    <div>
      <Button
        @toggle-btn-click="$emit('toggle-btn-click')"
        :text="!showAddTask ? 'Add task' : 'Close'"
        :color="!showAddTask ? 'green' : 'red'"
      />
    </div>
  </header>
</template>

<script>
import Button from "./Button.vue";
export default {
  name: "Header",
  props: {
    title: String,
    showAddTask: Boolean,
  },
  components: {
    Button,
  },
};
</script>

<style scoped>
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
</style>
