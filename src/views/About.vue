<template>
  <div class="about">
    <h3>Version 1.0.0</h3>
    <router-link to="/">Go Back</router-link>
  </div>
</template>

<script>
export default {
  name: "About",
  inheritAttrs: false, // disable 'non-props' warning
};
</script>

<style scoped>
.about {
  margin-top: 35px;
  padding: 20px;
  text-align: center;
}
</style>
