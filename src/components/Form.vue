<template>
  <div class="form-wrapper">
    <form>
      <div class="input-wrapper">
        <label for="task"></label>
        <input type="text" v-model="taskInput" maxlength="64" />
      </div>
      <div class="input-wrapper">
        <label for="date"></label>
        <input type="date" v-model="dateInput" />
      </div>
      <button class="btn" @click="addNewTask">{{ addTask }}</button>
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

<style scoped>
form {
  text-align: left;
  width: 100%;
}
.input-wrapper {
  display: inline-block;
  margin: 10px;
}
input[type='text'],
input[type='date'] {
  padding: 15px;
}

.btn {
  padding: 15px;
}
</style>
