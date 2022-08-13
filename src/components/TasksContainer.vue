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
  padding: 15px 30px;
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

.task-data {
  width: 50%;
}

.date-data {
  width: 10%;
}

td.date-data {
  font-size: 14px;
}

.tags-data {
  width: 30%;
}

.action-items {
  width: 10%;
}
</style>
