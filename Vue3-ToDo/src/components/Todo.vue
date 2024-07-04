<script setup>
import { ref, onMounted } from 'vue';
import TaskList from './TaskList.vue';
import TaskInput from './TaskInput.vue';

const tasks = ref([]);

const addTask = (task) => {
  tasks.value.push({ text: task, completed: false });
  saveTasksToLocalStorage();
};

const toggleTask = (index) => {
  tasks.value[index].completed = !tasks.value[index].completed;
  saveTasksToLocalStorage();
};

const removeTask = (index) => {
  tasks.value.splice(index, 1);
  saveTasksToLocalStorage();
};

function saveTasksToLocalStorage() {
  localStorage.setItem('tasks', JSON.stringify(tasks.value));
}

onMounted(() => {
  const savedTasks = localStorage.getItem('tasks');
  if (savedTasks) {
    tasks.value = JSON.parse(savedTasks);
  }
});
</script>

<template>
  <h2>To-Do List</h2>
  <div v-if="tasks.length === 0">No hay tareas. Agrega una nueva tarea para comenzar.</div>
  <TaskInput @addTask="addTask" />
  <TaskList :tasks="tasks" @toggleTask="toggleTask" @removeTask="removeTask" @editTask="editTask" />
</template>