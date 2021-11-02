<template>
  <!-- show massage task add -->
  <div
    :class="[
      isShowMessageAddTask ? 'show-massage-add' : '',
      'massage-contenr-add',
    ]"
  >
    <div class="massage-add" v-if="isShowMessageAddTask">
      <div class="massage-add-content">
        <p>{{ addTitle }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "MAdd",
  data() {
    return {
      addTitle: "Task has been added",
    };
  },
  props: {
    isShowMessageAddTask: Boolean,
  },
};
</script>

<style scoped>
.massage-contenr-add {
  position: absolute;
  top: 104%;
  left: 50%;
  transform: translate(-50%, -50%);
  transition: all 0.3s ease-in-out;
}
.show-massage-add {
  top: 95%;
}
.massage-add {
  background: #fff;
  /* padding: 10px 25px; */
  border-radius: 5px;
  box-shadow: 1px 1px 3px rgba(0, 0, 0, 0.4);
}

.massage-add-content {
  border-left: 5px solid green;
  padding: 10px 25px;
  border-radius: 5px;
}
</style>
