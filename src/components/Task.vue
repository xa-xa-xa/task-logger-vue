<template>
  <div
    @dblclick="$emit('toggle-reminder', task.id)"
    :class="[task.reminder ? 'reminder' : null, 'task']"
  >
    <h3>
      {{ task.text }}
      <i class="fas fa-times" @click="onDelete(task.id)"></i>
    </h3>
    <p>{{ task.day }}</p>
  </div>
</template>

<script>
export default {
  name: 'Task',
  props: {
    task: Object,
  },
  methods: {
    onDelete(id) {
      this.$emit('delete-task', id);
    },
  },
};
</script>

<style scope>
.fas {
  color: rgb(187, 0, 0);
  transition-duration: 0.3s;
}
.fas:hover {
  color: rgb(255, 0, 0);
  transform: rotate(270deg);
}
.task {
  background: #f4f4f4;
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
  border-left: 5px solid transparent;
  border-right: 5px solid transparent;
  border-radius: 5px;
  transition: 300ms;
}
.task.reminder {
  transition: 300ms;
  border-color:  rgb(103, 172, 0);
}
.task h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>
