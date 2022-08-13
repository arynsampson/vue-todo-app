<template>
  <div class="tasks-container">
    <table>
      <tr>
        <th class="task-data">Task</th>
        <th class="date-data">Due date</th>
        <th class="tags-data">Tags</th>
        <th class="action-item">#</th>
        <th class="action-item">#</th>
        <th class="action-item">#</th>
      </tr>
      <tbody>
        <Task
          v-for="(task, index) in tasks"
          :task="task.taskInput"
          :dateInput="task.dateInput"
          :key="index"
        />
      </tbody>
    </table>
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

<style>
.tasks-container {
  width: 100%;
  margin-top: 2rem;
}

table {
  width: 100%;
  text-align: left;
}

table,
th,
td {
  border: 1px solid rgba(0, 0, 0, 0.5);
  border-collapse: collapse;
  padding: 10px;
}

td.date-data {
  font-size: 14px;
}

.task-data {
  width: 50%;
}

.date-data {
  width: 10%;
}

.tags-data {
  width: 20%;
}

.action-item {
  width: 3%;
}
</style>
