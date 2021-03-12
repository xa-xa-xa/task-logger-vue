<template>
  <header>
    <h1>{{ title }}</h1>
    <Button
      v-show="onHomePage"
      @btn-click="$emit('toggle-add-task')"
      @click="onClick()"
      :text="!showTask ? 'Add Task' : 'Close'"
      :color="showTask ? 'red' : 'green'"
    />
    <!-- <Button text="Update task" color="blue" />
    <Button text="Delete task" color="red" /> -->
  </header>
</template>

<script>
import Button from './Button';
export default {
  name: 'Header',
  props: { title: String, showTask: Boolean },
  components: {
    Button,
  },
  computed: {
    onHomePage() {
      return this.$route.path === '/';
    },
  },
  methods: {
    async onClick() {
      this.$emit('toggle-add-task');
    },
  },
  // props: { title: {
  //     type: String,
  //     default: 'Hello World'
  // } },
  // props: ['title']
};
</script>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
button {
  border: none;
}
</style>
