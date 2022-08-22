<template>
  <div class="form-wrapper" v-if="!editTaskModal">
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
        <th class="action-item">Edit</th>
      </tr>
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index" :id="index" ref="item">
          <td :class="{ completed: task.isCompleted }">{{ task.task }}</td>
          <td class="task-actions">
            <i
              class="fa-solid fa-check"
              @click="completeTask(task)"
              v-if="!task.isCompleted"
            ></i>
          </td>
          <td class="task-actions">
            <i class="fa-solid fa-trash-can" @click="deleteTask(index)"></i>
          </td>
          <td class="task-actions">
            <i
              class="fa-solid fa-pen-to-square"
              @click="editTask(task, index)"
            ></i>
          </td>
        </tr>
      </tbody>
    </table>
  </div>

  <div class="edit-modal" v-if="editTaskModal">
    <p style="text-align: right" @click="closeEditModal">X</p>
    <h3>Edit modal</h3>
    <div class="form-wrapper">
      <form>
        <div class="input-wrapper">
          <label for="task"></label>
          <input type="text" v-model="taskInput" maxlength="64" required />
        </div>
        <button class="btn" @click="updateTask">Update task</button>
      </form>
    </div>
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
      editTaskModal: false,
      currentEditTaskIndex: 0,
    };
  },
  methods: {
    addNewTask(e) {
      e.preventDefault();
      this.tasks.push({ task: this.taskInput, isCompleted: false });
      this.taskInput = '';
    },
    completeTask(task) {
      task.isCompleted = true;
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
    editTask(task, index) {
      this.editTaskModal = true;
      this.currentEditTaskIndex = index;
      this.taskInput = this.tasks[index].task;
    },
    closeEditModal() {
      this.editTaskModal = false;
    },
    updateTask() {
      this.tasks[this.currentEditTaskIndex].task = this.taskInput;
      this.editTaskModal = false;
      this.taskInput = '';
    },
  },
  watch: {
    tasks: {
      handler() {
        localStorage.setItem('tasks', JSON.stringify(this.tasks));
      },
      deep: true,
    },
    taskInput() {
      if (this.editTaskModal) {
      }
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
  margin-top: 2rem;
}

table {
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

.edit-modal {
  width: 50%;
  margin: 0 auto;
  border: 1px solid black;
  border-radius: 20px;
  margin-top: 15px;
  padding: 20px;
}
</style>
