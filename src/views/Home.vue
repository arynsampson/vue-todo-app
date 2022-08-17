<template>
  <div class="form-wrapper">
    <form>
      <div class="input-wrapper">
        <label for="task"></label>
        <input type="text" v-model="taskInput" maxlength="64" required />
      </div>
      <button class="btn" @click="addNewTask">Add task</button>
    </form>
  </div>

  <div class="tasks-container">
    <table>
      <tr>
        <th class="task-data">Task</th>
        <th class="action-item">#</th>
        <th class="action-item">#</th>
      </tr>
      <tbody>
        <Task
          v-for="(task, index) in tasks"
          :task="task.taskInput"
          :key="index"
        />
      </tbody>
    </table>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: 'Home',
  components: {},
  data() {
    return {
      tasks: [],
    };
  },
  methods: {},
  mounted() {},
};
</script>

<style>
.home {
  width: 100%;
  margin: 0 auto;
}
form {
  width: 100%;
}
.input-wrapper {
  display: inline-block;
  margin: 10px;
}
input[type='text'] {
  width: 400px;
  padding: 15px;
}

.btn {
  padding: 15px;
}
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

.task-data {
  width: 20%;
}

.action-item {
  width: 2%;
}
</style>
