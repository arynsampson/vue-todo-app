<template>
  <button @click="testAdd">click</button>
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
      tasks: ['aryn'],
    };
  },
  methods: {
    toggleModal() {
      this.modalDisplay = !this.modalDisplay;
    },
    addTaskToArr(task) {
      this.tasks.push(task);
    },
    testAdd() {
      this.tasks.push('aryn');
    },
  },
  watch: {
    tasks: {
      deep: true,
      handler() {
        console.log(1);
      },
    },
  },
};
</script>

<style>
.home {
  width: 100%;
  margin: 0 auto;
}
</style>
