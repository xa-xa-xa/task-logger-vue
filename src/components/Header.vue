<template>
  <header>
    <h1>{{ title }}</h1>
    <Button @click="onClick()" text="Add task" color="green" />
    <!-- <Button text="Update task" color="blue" />
    <Button text="Delete task" color="red" /> -->
  </header>
</template>

<script>
import Button from './Button'
export default {
  name: 'Header',
    props: { title: String },
    components: {
        Button
    },
    methods: {
        onClick() {
            console.log('click')
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
