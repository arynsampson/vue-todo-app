<template>
  <div class="form-wrapper" v-if="!editTaskModal">
    <form>
      <div class="input-wrapper">
        <label for="task"></label>
        <input type="text" v-model="taskInput" maxlength="64" />
        <p class="error" v-if="errors[0].errorBool">
          {{ errors[0].taskError }}
        </p>
      </div>
      <div class="input-wrapper">
        <label for="dueDate"></label>
        <input type="date" v-model="dueDateInput" />
        <p class="error" v-if="errors[1].errorBool">
          {{ errors[1].dateError }}
        </p>
      </div>
      <button class="btn" @click="addNewTask">Add task</button>
    </form>
  </div>

  <div class="input-wrapper">
    <label for="search"></label>
    <input type="text" v-model="searchVal" maxlength="64" placeholder="search" />
  </div>

  <div class="tasks-container">
    <table>
      <tr>
        <th class="task-data">Task</th>
        <th class="task-due-date">Due Date</th>
        <th class="action-item">Complete</th>
      </tr>
      <tbody>
        <tr v-for="(task, index) in filteredTasks" :key="index" :id="index">
          <td :class="{ completed: task.isCompleted }">{{ task.task }}</td>
          <td :class="{ completed: task.isCompleted }">{{ task.dueDate }}</td>
          <td class="task-actions">
            <div @click="toggleContextMenu(task, index)" class="context-menu-cell">
              <p class="context-menu-toggle">CM</p>
              <div class="context-menu">
                <Context v-if="task.contextMenu" :task="task" :index="index" :id="index" />
              </div>
            </div>
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

<script setup>
import { ref, reactive, computed, watch, onMounted } from 'vue';
import Context from '../components/context.vue';

const taskInput = ref('');
const dueDateInput = ref(null);
const errors = reactive([
  { taskError: 'Please enter some text', errorBool: false },
  { dateError: 'Please enter a date', errorBool: false },
]);
const tasks = ref([]);
const editTaskModal = ref(false);
const currentEditTaskIndex = ref(0);
const searchVal = ref('');

const toggleContextMenu = (currTask, index) => {
  tasks.value.forEach((task) => {
    if (tasks.value.indexOf(task) !== index) {
      task.contextMenu = false;
    } else {
      currTask.contextMenu = !currTask.contextMenu;
    }
  });
};

const addNewTask = (e) => {
  e.preventDefault();
  if (!taskInput.value) {
    errors[0].errorBool = true;
  } else if (!dueDateInput.value) {
    errors[1].errorBool = true;
  } else {
    tasks.value.push({
      task: taskInput.value,
      dueDate: dueDateInput.value,
      isCompleted: false,
      contextMenu: false,
    });
    taskInput.value = '';
    dueDateInput.value = '';
    errors[0].errorBool = false;
    errors[1].errorBool = false;
  }
};

const completeTask = (task) => {
  task.isCompleted = true;
};

const deleteTask = (index) => {
  tasks.value.splice(index, 1);
};

const editTask = (task, index) => {
  editTaskModal.value = true;
  currentEditTaskIndex.value = index;
  taskInput.value = tasks.value[index].task;
  dueDateInput.value = tasks.value[index].dueDate;
};

const updateTask = (e) => {
  e.preventDefault();
  tasks.value[currentEditTaskIndex.value].task = taskInput.value;
  tasks.value[currentEditTaskIndex.value].dueDate = dueDateInput.value;
  editTaskModal.value = false;
  taskInput.value = '';
  dueDateInput.value = '';
};

const closeEditModal = () => {
  editTaskModal.value = false;
};

const filteredTasks = computed(() => {
  return tasks.value.filter((item) => item.task.includes(searchVal.value));
});

watch(
  tasks,
  (newVal, oldVal) => {
    localStorage.setItem('tasks', JSON.stringify(tasks.value));
  },
  {
    deep: true,
  }
);

onMounted(() => {
  if (!localStorage.getItem('tasks')) {
    localStorage.setItem('tasks', JSON.stringify(tasks.value));
  } else {
    tasks.value = JSON.parse(localStorage.getItem('tasks'));
  }
});
</script>

<style>
.home {
  width: 100%;
  margin: 0 auto;
}
form {
  width: 100%;
  height: 150px;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: flex-start;
}
.input-wrapper {
  display: inline-block;
  margin: 0 10px;
  height: 150px;
}
input[type='text'],
input[type='date'] {
  width: 450px;
  padding: 15px;
  box-sizing: border-box;
}

.btn {
  padding: 15px;
}

.error {
  margin: 10px;
  color: red;
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

.context-menu-cell {
  position: relative;
}

.context-menu-toggle {
  margin: 0;
}

.context-menu {
  position: absolute;
  left: 70px;
  top: -20px;
  z-index: 1;
  /* padding: 0;
  margin: 0; */
}
</style>
