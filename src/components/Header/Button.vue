<template>
  <button
    :style="{ background: color }"
    class="btn"
    @click="onClick()"
    data-toggle="add task"
    type="button"
    v-show="homePage"
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
  methods: {
    onClick() {
      this.$emit("toggle-btn-click");
    },
  },
  computed: {
    homePage() {
      if (this.$route.path == "/") {
        return true;
      } else {
        return false;
      }
    },
  },
};
</script>
