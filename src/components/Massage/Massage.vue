<template>
  <div class="massage">
    <!-- show massage task delete -->
    <MDelete
      :isShowMessageTask="isShowMessageTask"
      @delete-task="$emit('delete-task')"
      @isShow-massage-task="$emit('isShow-massage-task')"
    />
    <!-- show massage task add -->
    <MAdd :isShowMessageAddTask="isShowMessageAddTask" />
  </div>
</template>

<script>
import MAdd from "./MAdd.vue";
import MDelete from "./MDelete.vue";
export default {
  name: "Massage",
  props: {
    isShowMessageAddTask: Boolean,
    isShowMessageTask: Boolean,
  },
  components: {
    MAdd,
    MDelete,
  },
  emits: ["delete-task", "isShow-massage-task"],
};
</script>
