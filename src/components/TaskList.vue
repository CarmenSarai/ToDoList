<template>
  <div>
    <add-task @task-added="fetchTasks"></add-task>
    <div v-for="task in tasks" :key="task.id">
      <task-item
        :task="task"
        @task-updated="fetchTasks"
        @task-deleted="fetchTasks"
      ></task-item>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import AddTask from "./AddTask.vue";
import TaskItem from "./TaskItem.vue";

export default {
  components: {
    AddTask,
    TaskItem,
  },
  data() {
    return {
      tasks: [],
    };
  },
  created() {
    this.fetchTasks();
  },
  methods: {
    fetchTasks() {
      axios
        .get(
          "https://886847c2-af09-4b28-b9b2-67c5e93ae16e-00-31upf5wobvlg5.riker.replit.dev/api/tasks/",
        )
        .then((response) => {
          this.tasks = response.data;
        })
        .catch((error) => {
          console.error("Error fetching tasks:", error);
        });
    },
  },
};
</script>
