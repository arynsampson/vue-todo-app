<template>
  <div>
    <p>{{ task }}</p>
    <p>{{ dateInput }}</p>
  </div>
  <hr />
</template>

<script>
export default {
  name: 'Task',
  props: ['task', 'dateInput', 'key'],
};
</script>

<style></style>
