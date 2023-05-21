<template>
  <div id="app">
    <h1>Tasks</h1>
    <TaskProgress :progress="progress"></TaskProgress>
    <NewTask @taskAdded="addTask"></NewTask>
    <TaskGrid
      :tasks="tasks"
      @deleteTask="deleteTask"
      @changeStatus="changeStatus"
    ></TaskGrid>
  </div>
</template>

<script>
import TaskGrid from "./components/TaskGrid.vue";
import TaskProgress from "./components/TaskProgress.vue";
import NewTask from "./components/NewTask.vue";

export default {
  components: { TaskGrid, NewTask, TaskProgress },

  data() {
    return {
      tasks: [],
    };
  },

  watch: {
    tasks: {
      deep: true,
      handler(values) {
        localStorage.setItem("tasks", JSON.stringify(values));
      },
    },
  },

  computed: {
    progress() {
      const total = this.tasks.length;
      const done = this.tasks.filter((t) => !t.pending).length;

      return Math.round((done / total) * 100) || 0;
    },
  },

  methods: {
    addTask(newTask) {
      const hasTask = this.tasks.some((t) => t.name === newTask.name);

      if (!hasTask) {
        this.tasks.push({ ...newTask, pending: true });
      }
    },

    deleteTask(taskId) {
      this.tasks.splice(taskId, 1);
    },

    changeStatus(id) {
      this.tasks[id].pending = !this.tasks[id].pending;
    },
  },

  beforeMount() {
    const json = localStorage.getItem("tasks");
    const tasks = JSON.parse(json);

    if (Array.isArray(tasks)) {
      this.tasks = tasks;
    } else {
      this.tasks = [];
    }
  },
};
</script>

<style>
body {
  font-family: "Lato", sans-serif;
  background: linear-gradient(to right, rgb(22, 34, 42), rgb(58, 96, 115));
  color: #fff;
}

#app {
  display: flex;
  flex: 1;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

#app h1 {
  margin-bottom: 5px;
  font-weight: 300;
  font-size: 3rem;
}
</style>
