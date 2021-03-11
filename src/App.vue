<template>
  <div class="container">
    <Header
      title="Task Logger"
      @toggle-add-task="toggleAddTask"
      :showTask="showAddTasks"
    />
    <div v-show="showAddTasks">
      <AddTask @add-task="addTask" />
    </div>
    <Tasks
      :tasks="tasks"
      @delete-task="deleteTask"
      @toggle-reminder="toggleReminder"
    />
  </div>
</template>

<script>
// imports
import Header from './components/Header';
import Tasks from './components/Tasks';
import AddTask from './components/AddTask';

export default {
  name: 'App',
  components: {
    Header,
    Tasks,
    AddTask,
  },
  data() {
    return {
      tasks: [],
      showAddTasks: false,
    };
  },
  methods: {
    toggleAddTask() {
      this.showAddTasks = !this.showAddTasks;
    },
    addTask(task) {
      this.tasks = [...this.tasks, task];
    },
    deleteTask(id) {
      if (
        confirm(
          `You are about to delete "${
            this.tasks.find((t) => t.id === id).text
          }" task. Are you sure?`
        )
      )
        this.tasks = this.tasks.filter((t) => t.id !== id);
    },
    toggleReminder(id) {
      this.tasks = [...this.tasks].map((task) =>
        task.id === id
          ? { ...task, reminder: task.reminder ? false : true }
          : task
      );
    },
  },
  created() {
    this.tasks = [
      {
        id: 1,
        text: 'Doctors Appointment',
        day: 'March 1st at 1:30pm',
        reminder: false,
      },
      {
        id: 2,
        text: 'Meeting at work',
        day: 'March 5th at 4:30pm',
        reminder: false,
      },
    ];
  },
};
</script>

<style>
/* Global Styles */
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
#app {
  /* font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale; */
  /* text-align: center; */
  color: #2c3e50;
  /* margin-top: 60px; */
}
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Poppins', sans-serif;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
.btn {
  display: block;
  background: #000;
  color: #fff;
  padding: 10px 20px;
  margin: 15px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}

.btn:focus {
  outline: none;
}
.btn-block {
  display: block;
  width: 100%;
}
</style>
