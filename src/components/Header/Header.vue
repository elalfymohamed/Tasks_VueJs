<template>
  <header class="header">
    <div>
      <h1>{{ title }}</h1>
    </div>
    <div>
      <Button text="Add Task" color="green" />
    </div>
  </header>
</template>

<script>
import Button from "./Button.vue";
export default {
  name: "Header",
  props: {
    title: String,
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
