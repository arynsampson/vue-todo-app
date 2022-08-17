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
        <th class="action-item">Complete</th>
        <th class="action-item">Delete</th>
      </tr>
      <tbody>
        <tr
          v-for="(task, index) in tasks"
          :key="index"
          :id="index"
          :class="{ completed: task.isCompleted }"
          ref="item"
        >
          <td>{{ task.task }}</td>
          <td class="task-actions">
            <i
              class="fa-solid fa-check"
              @click="completeTask($event, task)"
            ></i>
          </td>
          <td class="task-actions">
            <i
              class="fa-solid fa-trash-can"
              @click="deleteTask($event, index)"
            ></i>
          </td>
        </tr>
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
      taskInput: '',
      tasks: [],
    };
  },
  methods: {
    addNewTask(e) {
      e.preventDefault();
      this.tasks.push({ task: this.taskInput, isCompleted: false });
      this.taskInput = '';
    },
    completeTask($event, task, index) {
      task.isCompleted = true;
    },
    deleteTask($event, index) {
      this.tasks.splice(index, 1);
    },
  },
  watch: {
    tasks: {
      handler() {
        localStorage.setItem('tasks', JSON.stringify(this.tasks));
      },
      deep: true,
    },
  },
  mounted() {
    if (!localStorage.getItem('tasks')) {
      localStorage.setItem('tasks', JSON.stringify(this.tasks));
    } else {
      this.tasks = JSON.parse(localStorage.getItem('tasks'));
    }
  },
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
  width: 1%;
  text-align: center;
}

.task-actions {
  text-align: center;
}

i:hover {
  cursor: pointer;
}

.completed {
  opacity: 0.3;
}
</style>
