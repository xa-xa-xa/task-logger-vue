<template>
  <AddTask v-show="showAddTasks" @add-task="addTask" />
  <Tasks
    :tasks="tasks"
    @delete-task="deleteTask"
    @toggle-reminder="toggleReminder"
  />
</template>

<script>
import Tasks from '../components/Tasks';
import AddTask from '../components/AddTask';

export default {
  name: 'Home',
  props: {
    showAddTasks: Boolean,
  },
  components: {
    Tasks,
    AddTask,
  },
  data: () => ({ tasks: [] }),
  methods: {
    async addTask(task) {
      const res = await fetch('api/tasks', {
        method: 'POST',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(task),
      });
      const data = await res.json();
      this.tasks = [...this.tasks, data];
    },
    async deleteTask(id) {
      if (
        confirm(
          `You are about to delete "${
            this.tasks.find((t) => t.id === id).text
          }" task. Are you sure?`
        )
      ) {
        const res = await fetch(`api/tasks/${id}`, {
          method: 'DELETE',
        });
        res.status === 200
          ? (this.tasks = this.tasks.filter((t) => t.id !== id))
          : alert('Could not delete task');
      }
    },
    async toggleReminder(id) {
      const taskToggle = await this.fetchTask(id);
      const updatedTask = { ...taskToggle, reminder: !taskToggle.reminder };
      const res = await fetch(`api/tasks/${id}`, {
        method: 'PUT',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(updatedTask),
      });

      const data = await res.json();

      this.tasks = [...this.tasks].map((task) =>
        task.id === id ? { ...task, reminder: data.reminder } : task
      );
    },
    async fetchTask(id) {
      const res = await fetch(`api/tasks/${id}`);
      const data = await res.json();
      return data;
    },
  },

  async created() {
    const fetchedData = await fetch('api/tasks');
    const data = await fetchedData.json();
    this.tasks = data;
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
