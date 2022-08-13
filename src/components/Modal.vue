<template>
  <div class="modal-backdrop" @click.self="closeModal">
    <div class="modal">
      <h3 class="modal-heading">Edit task</h3>
      <Form />
    </div>
  </div>
</template>

<script>
import Form from './Form.vue';

export default {
  name: 'Modal',
  components: {
    Form,
  },
  methods: {
    closeModal() {
      this.$emit('close');
    },
  },
  emits: ['close'],
};
</script>

<style scoped>
.modal-backdrop {
  background: rgba(0, 0, 0, 0.5);
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal {
  width: 500px;
  height: 300px;
  background: #fff;
}

.modal-heading {
  font-size: 30px;
}
</style>
