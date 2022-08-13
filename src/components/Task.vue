<template>
  <tr>
    <td class="task-data">{{ task }}</td>
    <td class="date-data">{{ dateInput }}</td>
    <td class="tags-data">html,css,js</td>
    <td class="action-item">#</td>
    <td class="action-item">#</td>
    <td class="action-item">#</td>
  </tr>
</template>

<script>
export default {
  name: 'Task',
  props: ['task', 'dateInput', 'key'],
};
</script>

<style></style>
