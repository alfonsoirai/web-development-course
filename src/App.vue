<template>
   <div class="md-layout md-gutter">
    <div class="md-layout-item"></div>
    <div class="md-layout-item">
      <h2>My todo app</h2>
      <form @submit.prevent="addTask">
        <input v-model="newTaskName" type="text">
        <md-button class="md-raised md-primary" type="submit">Add task</md-button>
      </form>

      <task-list :title="'Pendings'" :task-list="tasksPending" @complete="toggleTasks"/>
    <hr>

    <task-list :title="'Completed'" :task-list="tasksCompleted" @complete="toggleTasks"/>
    </div>
    <div class="md-layout-item"></div>
  </div>
</template>

<script>
import TaskList from "./components/TaskList";


export default {
  components: {
    TaskList
  },

  data() {
    return {
      newTaskName: "",
      tasks: []
    };
  },
  methods: {
    toggleTasks(task) {
      task.done = !task.done;
    },
    addTask() {
      if (!this.newTaskName) return;
      this.tasks.push({ name: this.newTaskName, done: false });
      this.newTaskName = "";
    },
  },
  mounted() {
      console.log('App mounted!');
      if (localStorage.getItem('tasks')) this.tasks = JSON.parse(localStorage.getItem('tasks'));
    },
    watch: {
      tasks: {
        handler() {
        console.log('Todos changed!');
        localStorage.setItem('tasks', JSON.stringify(this.tasks));
        },
      deep: true,
      },
    },
  computed: {
    tasksPending() {
      return this.tasks.filter(task => !task.done);
    },
    tasksCompleted() {
      return this.tasks.filter(task => task.done);
    }
  }
};
</script>

