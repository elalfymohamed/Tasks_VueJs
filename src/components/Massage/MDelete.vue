<template>
  <div class="massage">
    <!-- show massage task delete -->
    <div class="massage-contenrt" v-if="isShowMessageTask">
      <div class="massage-delete">
        <div class="massage-delete-content">
          <h4 class="massage-delete-title">
            are you sure you want to delete this task?
          </h4>
          <div class="massage-delete-btn">
            <button
              type="button"
              data-toggle="yes"
              @click="
                {
                  onDeleteTask();
                  isShowMassege();
                }
              "
            >
              Yes
            </button>
            <button type="button" data-toggle="no" @click="isShowMassege()">
              No
            </button>
          </div>
        </div>
      </div>
    </div>
    <!-- show massage task add -->
    <div
      :class="[
        isShowMessageAddTask ? 'show-massage-add' : '',
        'massage-contenr-add',
      ]"
    >
      <div class="massage-add" v-if="isShowMessageAddTask">
        <div class="massage-add-content">
          <p>Task has been added</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "MDelete",
  props: {
    isShowMessageTask: Boolean,
    isShowMessageAddTask: Boolean,
  },
  methods: {
    isShowMassege() {
      this.$emit("isShow-massage-task");
    },
    onDeleteTask() {
      this.$emit("delete-task");
    },
  },
};
</script>

<style scoped>
.massage-contenrt {
  background: rgba(0, 0, 0, 0.4);
  max-width: 100vw;
  height: 100vh;
  margin: 0 auto;
  position: fixed;
  inset: 0;
}
.massage-delete {
  background: #fff;
  padding: 40px 60px;
  border-radius: 5px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
.massage-delete-content {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.massage-delete-title {
  font-size: 1em;
  font-weight: 400;
  /* text-align: center; */
  margin-bottom: 20px;
}
.massage-delete-btn {
  display: flex;
  justify-content: space-evenly;
  align-items: center;
  width: 100%;
  margin-top: 20px;
}
.massage-delete-btn button {
  background: transparent;
  border: 1px solid rgb(0, 128, 0);
  color: rgb(0, 0, 0);
  padding: 5px 15px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 1rem;
  font-weight: 400;
  font-family: inherit;
  transition: all 0.3s ease-in-out;
}
.massage-delete-btn button:last-child {
  border: 1px solid rgb(255, 0, 0);
}
.massage-delete-btn button:hover {
  background-color: rgb(0, 128, 0);
  color: #fff;
}
.massage-delete-btn button:last-child:hover {
  background-color: rgb(255, 0, 0);
  color: #fff;
}

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
