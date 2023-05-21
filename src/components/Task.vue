<template>
  <div class="task" :class="stateClass" @click="$emit('changeStatus')">
    <span class="close" @click.stop="$emit('closeTask', task)">x</span>
    <p>{{ task.name }}</p>
  </div>
</template>

<script>
export default {
  props: {
    task: { type: Object, required: true },
  },

  computed: {
    stateClass() {
      return {
        pending: this.task.pending,
        done: !this.task.pending,
      };
    },
  },
};
</script>

<style>
.task {
  box-sizing: border-box;
  width: 350px;
  height: 150px;
  padding: 10px;
  border-radius: 8px;
  font-size: 2rem;
  font-weight: 300;
  cursor: pointer;
  user-select: none;
  display: flex;
  justify-content: center;
  align-items: center;
}

.pending {
  border-left: 12px solid rgb(94, 2, 2);
  background-color: red;
}

.done {
  color: #ddd;
  text-decoration: line-through;
  border-left: 12px solid darkgreen;
  background-color: rgb(8, 238, 8);
}

.pending .close {
  background-color: rgb(94, 2, 2);
}

.done .close {
  background-color: darkgreen;
}

.close {
  position: absolute;
  right: 10px;
  top: 10px;
  font-size: 0.9rem;
  font-weight: 600;
  height: 20px;
  width: 20px;
  border-radius: 10px;
  display: flex;
  justify-content: center;
}
</style>
