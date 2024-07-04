<template>
  <div class="container">
    <h1>TO-DO</h1>
    <TaskInput @add-task="addTask" />
    <TaskList
        :tasks="tasks"
        @toggle-task="toggleTask"
        @remove-task="removeTask"
        @edit-task="editTask"
    />
  </div>
</template>

<script>
import TaskInput from './components/TaskInput.vue';
import TaskList from './components/TaskList.vue';

export default {
  components: {
    TaskInput,
    TaskList
  },
  data() {
    return {
      tasks: []
    };
  },
  mounted() {
    this.loadTasks();
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=2')
        .then(response => response.json())
        .then(data => {
          const apiTasks = data.map(task => ({
            id: task.id,
            text: task.title,
            completed: task.completed
          }));

          this.tasks = [...this.tasks, ...apiTasks];
          this.saveTasks();
        });
  },
  methods: {
    addTask(task) {
      this.tasks.push({ id: Date.now(), text: task, completed: false });
      this.saveTasks();
    },
    toggleTask(task) {
      task.completed = !task.completed;
      this.saveTasks();
    },
    removeTask(task) {
      this.tasks = this.tasks.filter(t => t.id !== task.id);
      this.saveTasks();
    },
    editTask(task, newText) {
      task.text = newText;
      this.saveTasks();
    },
    saveTasks() {
      localStorage.setItem('tasks', JSON.stringify(this.tasks));
    },
    loadTasks() {
      const tasks = localStorage.getItem('tasks');
      if (tasks) {
        this.tasks = JSON.parse(tasks);
      }
    }
  }
};
</script>
