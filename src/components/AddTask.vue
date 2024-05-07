<template>
  <div>
    <input
      v-model="newTask"
      placeholder="Add new task"
      @keyup.enter="addTask"
    />
    <button @click="addTask">Add Task</button>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      newTask: "",
    };
  },
  methods: {
    addTask() {
      if (this.newTask.trim()) {
        axios
          .post(
            "https://886847c2-af09-4b28-b9b2-67c5e93ae16e-00-31upf5wobvlg5.riker.replit.dev/api/tasks/",
            {
              title: this.newTask,
            },
          )
          .then((response) => {
            this.$emit("task-added");
            this.newTask = "";
          })
          .catch((error) => {
            console.error("Error adding task:", error);
          });
      }
    },
  },
};
</script>
