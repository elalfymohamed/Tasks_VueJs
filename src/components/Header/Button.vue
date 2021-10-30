<template>
  <button
    :style="{ background: color }"
    class="btn"
    data-toggle="add task"
    type="button"
  >
    {{ text }}
  </button>
</template>

<script>
export default {
  name: "Button",
  props: {
    text: String,
    color: String,
  },
};
</script>
