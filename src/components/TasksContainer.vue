<template>
  <div class="tasks-container">
    <Task
      v-for="(task, index) in tasks"
      :task="task.taskInput"
      :dateInput="task.dateInput"
      :key="index"
    />
  </div>
</template>

<script>
import Task from './Task.vue';

export default {
  name: 'TasksContainer',
  components: {
    Task,
  },
  props: ['tasks'],
  data() {
    return {};
  },
};
</script>

<style></style>
