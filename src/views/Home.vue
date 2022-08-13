<template>
  <div class="home">
    <Form
      addTask="Add task"
      :modalDisplay="modalDisplay"
      @newTask="addTaskToArr"
    />
    <!-- <div>
      <button @click="toggleModal">Open modal</button>
      <Modal v-if="modalDisplay" @close="toggleModal" />
    </div> -->
  </div>

  <TasksContainer :tasks="tasks" />
</template>

<script>
// @ is an alias to /src
import Modal from '@/components/Modal.vue';
import Form from '@/components/Form.vue';
import TasksContainer from '@/components/TasksContainer.vue';

export default {
  name: 'Home',
  components: { Modal, Form, TasksContainer },
  data() {
    return {
      modalDisplay: false,
      tasks: [],
    };
  },
  methods: {
    toggleModal() {
      this.modalDisplay = !this.modalDisplay;
    },
    addTaskToArr(task) {
      this.tasks.push(task);
    },
  },
  watch: {
    tasks() {
      console.log(1);
    },
  },
};
</script>
