<template>
  <div class="container mt-4">
    <TaskForm @addTask="addTask" />
    <task-list
      :tasks="tasks"
      @delete="deleteTask"
      @update-task="updateTask"
      @toggleCompleted="toggleCompleted"
    />
  </div>
</template>

<script>
import TaskForm from "@/components/TaskForm";
import TaskList from "@/components/TaskList.vue";
import axios from "axios";

export default {
  components: {
    TaskForm,
    TaskList,
  },
  data() {
    return {
      tasks: [],
    };
  },
  methods: {
    async fetchTasks() {
      try {
        const response = await axios.get(
          "https://jsonplaceholder.typicode.com/todos",
          {
            params: {
              _limit: 7,
            },
          }
        );
        this.tasks = response.data;
      } catch (e) {
        alert("Ошибка!");
      }
    },
    addTask(task) {
      this.tasks.push(task);
    },
    deleteTask(task) {
      this.tasks = this.tasks.filter((t) => t.id !== task.id);
    },
    updateTask(payload) {
      this.tasks.forEach((task) => {
        if (task.title === payload.taskTitle) {
          task.title = payload.editedTitle;
        }
      });
    },
    toggleCompleted(id) {
      this.tasks.forEach((task) => {
        if (task.id === id) {
          task.completed = !task.completed;
        }
      });
    },
  },
  mounted() {
    this.fetchTasks();
  },
};
</script>

<style>
* {
  /* margin: 0;
  padding: 0; */
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
