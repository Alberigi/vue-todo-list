<template>
  <div class="task-grid">
    <template v-if="tasks.length">
      <Task
        v-for="(task, id) in tasks"
        :key="id"
        :task="task"
        @closeTask="$emit('deleteTask', id)"
        @changeStatus="$emit('changeStatus', id)"
      ></Task>
    </template>
    <p v-else class="no-task">your life is up to date</p>
  </div>
</template>

<script>
import Task from "./Task.vue";

export default {
  components: { Task },

  props: {
    tasks: { type: Array, required: true },
  },
};
</script>

<style>
.task-grid {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}

.task-grid .task {
  margin: 10px;
}

.no-task {
  color: #aaa;
  font-size: 1.7rem;
}
</style>
