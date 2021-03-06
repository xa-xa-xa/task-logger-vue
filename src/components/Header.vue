<template>
  <header>
    <h1>{{ title }}</h1>
    <Button
      @toggle-add-task="$emit('toggle-add-task')"
      @click="onClick()"
      :text="show"
      color="green"
    />
    <!-- <Button text="Update task" color="blue" />
    <Button text="Delete task" color="red" /> -->
  </header>
</template>

<script>
import Button from './Button';

// let show = false;
export default {
  name: 'Header',
  props: { title: String, showTask: Boolean },
  components: {
    Button,
  },
  methods: {
    async onClick() {
      this.$emit('toggle-add-task');
    },
  },
  computed: {
    show : function(){
      // TODO Show conditional rendering on button
      return this.showTask ? "Close" : "Add Task"
    }
  }
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
</style>
