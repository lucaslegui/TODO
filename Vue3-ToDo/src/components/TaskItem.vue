<template>
  <li class="list-group-item d-flex flex-column align-items-start">
    <span :class="{ completed: task.completed }" @click="toggleTask">{{ task.text }}</span>
    <div class="button-group mt-2">
      <button @click="toggleTask" class="btn btn-success">{{ task.completed ? 'Marcar como incompleta' : 'Marcar como completada' }}</button>
      <button @click="removeTask" class="btn btn-danger">Eliminar</button>
      <button @click="editTask" class="btn btn-warning">Editar</button>
    </div>
  </li>
</template>

<script>
export default {
  props: {
    task: Object
  },
  methods: {
    toggleTask() {
      this.$emit('toggle-task', this.task);
    },
    removeTask() {
      this.$emit('remove-task', this.task);
    },
    editTask() {
      const newText = prompt('Editar tarea:', this.task.text);
      if (newText !== null) {
        this.$emit('edit-task', this.task, newText);
      }
    }
  }
};
</script>
