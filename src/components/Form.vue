<template>
  <div class="form-wrapper">
    <form>
      <div>
        <label for="task"></label>
        <input type="text" v-model="taskInput" />
      </div>
      <div>
        <label for="date"></label>
        <input type="date" v-model="dateInput" />
      </div>

      <br />
      <button @click="addNewTask">{{ addTask }}</button>
    </form>
  </div>
</template>

<script>
export default {
  name: 'Form',
  props: ['addTask', 'modalDisplay', 'editTask'],
  data() {
    return {
      taskInput: '',
      dateInput: '',
      currentTask: null,
    };
  },
  emits: ['newTask'],
  methods: {
    addNewTask(e) {
      e.preventDefault();
      this.currentTask = {
        taskInput: this.taskInput,
        dateInput: this.dateInput,
        isCompleted: false,
      };
      this.$emit('newTask', this.currentTask);
      this.taskInput = '';
      this.dateInput = '';
      this.currentTask = null;
    },
  },
};
</script>

<style></style>
