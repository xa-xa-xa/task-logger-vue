<template>
  <div class="home">
    <AddTask v-show="showAddTasks" @add-task="addTask" />
    <Tasks
      :tasks="tasks"
      @delete-task="deleteTask"
      @toggle-reminder="toggleReminder"
    />
  </div>
</template>

<script>
// @ is an alias to /src
import Tasks from "@/components/Tasks";
import AddTask from "@/components/AddTask";

export default {
  name: "Home",
  props: {
    showAddTasks: Boolean
  },
  components: {
    Tasks,
    AddTask
  },
  data: () => ({ tasks: [] }),
  methods: {
    async addTask(task) {
      const res = await fetch("api/tasks", {
        method: "POST",
        headers: {
          "Content-type": "application/json"
        },
        body: JSON.stringify(task)
      });
      const data = await res.json();
      this.tasks = [...this.tasks, data];
    },
    async deleteTask(id) {
      if (
        confirm(
          `You are about to delete "${
            this.tasks.find(t => t.id === id).text
          }" task. Are you sure?`
        )
      ) {
        const res = await fetch(`api/tasks/${id}`, {
          method: "DELETE"
        });
        res.status === 200
          ? (this.tasks = this.tasks.filter(t => t.id !== id))
          : alert("Could not delete task");
      }
    },
    async toggleReminder(id) {
      const taskToggle = await this.fetchTask(id);
      const updatedTask = { ...taskToggle, reminder: !taskToggle.reminder };
      const res = await fetch(`api/tasks/${id}`, {
        method: "PUT",
        headers: {
          "Content-type": "application/json"
        },
        body: JSON.stringify(updatedTask)
      });

      const data = await res.json();

      this.tasks = [...this.tasks].map(task =>
        task.id === id ? { ...task, reminder: data.reminder } : task
      );
    },
    async fetchTask(id) {
      const res = await fetch(`api/tasks/${id}`);
      const data = await res.json();
      return data;
    }
  },

  async created() {
    const fetchedData = await fetch("api/tasks");
    const data = await fetchedData.json();
    this.tasks = data;
  }
};
</script>
