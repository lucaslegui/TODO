<template>
  <ul class="list-group">
    <TaskItem
        v-for="task in tasks"
        :key="task.id"
        :task="task"
        @toggle-task="toggleTask"
        @remove-task="removeTask"
        @edit-task="editTask"
    />
  </ul>
</template>

<script>
import TaskItem from './TaskItem.vue';

export default {
  components: {
    TaskItem
  },
  props: {
    tasks: Array
  },
  methods: {
    toggleTask(task) {
      this.$emit('toggle-task', task);
    },
    removeTask(task) {
      this.$emit('remove-task', task);
    },
    editTask(task, newText) {
      this.$emit('edit-task', task, newText);
    }
  }
};
</script>