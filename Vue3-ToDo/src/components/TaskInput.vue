<template>
  <div>
    <input v-model="newTask" placeholder="Nueva tarea" class="form-control mb-3 task-input">
    <button @click="addTask" class="btn btn-primary add-btn">Agregar Tarea</button>
  </div>
</template>


<script>
export default {
  data() {
    return {
      newTask: ''
    };
  },
  methods: {
    addTask() {
      if (this.newTask.trim() !== '') {
        this.$emit('add-task', this.newTask);
        this.newTask = '';
      }
    }
  }
};
</script>