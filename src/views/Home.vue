<template>
  <div class="form-wrapper" v-if="!editTaskModal">
    <form>
      <div class="input-wrapper">
        <label for="task"></label>
        <input type="text" v-model="taskInput" maxlength="64" />
        <span v-if="errors.taskErrorBool">{{ errors[0].taskError }}</span>
      </div>
      <div class="input-wrapper">
        <label for="dueDate"></label>
        <input type="date" v-model="dueDateInput" />
        <span v-if="errors.dateErrorBool">{{ errors[1].dateError }}</span>
      </div>
      <button class="btn" @click="addNewTask">Add task</button>
    </form>
  </div>

  <div class="input-wrapper">
    <label for="search"></label>
    <input
      type="text"
      v-model="searchVal"
      maxlength="64"
      placeholder="search"
    />
  </div>

  <div class="tasks-container">
    <table>
      <tr>
        <th class="task-data">Task</th>
        <th class="task-due-date">Due Date</th>
        <th class="action-item">Complete</th>
        <th class="action-item">Delete</th>
        <th class="action-item">Edit</th>
      </tr>
      <tbody>
        <tr
          v-for="(task, index) in filteredTasks"
          :key="index"
          :id="index"
          ref="item"
        >
          <td :class="{ completed: task.isCompleted }">{{ task.task }}</td>
          <td :class="{ completed: task.isCompleted }">{{ task.dueDate }}</td>
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
              v-if="!task.isCompleted"
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
        <div class="input-wrapper">
          <label for="dueDate"></label>
          <input type="date" v-model="dueDateInput" required />
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
      dueDateInput: '',
      errors: [
        { taskError: 'Please enter some text', taskErrorBool: false },
        { dateError: 'Please enter a date', dateErrorBool: false },
      ],
      tasks: [],
      editTaskModal: false,
      currentEditTaskIndex: 0,
      searchVal: '',
    };
  },
  methods: {
    addNewTask(e) {
      e.preventDefault();
      if (!this.taskInput) {
        this.errors.taskErrorBool = true;
      } else if (!this.dueDateInput) {
        this.errors.dateErrorBool = true;
      } else {
        this.tasks.push({
          task: this.taskInput,
          dueDate: this.dueDateInput,
          isCompleted: false,
        });
        this.taskInput = '';
        this.dueDateInput = '';
        this.errors.taskErrorBool = false;
        this.errors.dateErrorBool = false;
      }
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
      this.dueDateInput = this.tasks[index].dueDate;
    },
    closeEditModal() {
      this.editTaskModal = false;
    },
    updateTask() {
      this.tasks[this.currentEditTaskIndex].task = this.taskInput;
      this.tasks[this.currentEditTaskIndex].dueDate = this.dueDateInput;
      this.editTaskModal = false;
      this.taskInput = '';
      this.dueDateInput = '';
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
  computed: {
    filteredTasks() {
      return this.tasks.filter((item) => item.task.includes(this.searchVal));
    },
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
input[type='text'],
input[type='date'] {
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

.task-due-date {
  width: 4%;
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
