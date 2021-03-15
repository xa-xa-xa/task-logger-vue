<template>
  <div class="container">
    <Header
      title="Task Logger"
      @toggle-add-task="toggleAddTask"
      :showTask="showAddTasks"
    />
    <router-view :showAddTasks="showAddTasks"> </router-view>
    <Footer />
  </div>
</template>

<script>
import Header from './components/Header';
import Footer from './components/Footer';

export default {
  name: 'App',
  components: {
    Header,
    Footer,
  },
  data() {
    return {
      showAddTasks: false,
    };
  },
  methods: {
    toggleAddTask() {
      this.showAddTasks = !this.showAddTasks;
    },
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
  color: #2c3e50;
}
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Poppins', sans-serif;
  height: 100vh;
  background: repeating-linear-gradient(
    -45deg,
    rgb(223, 235, 228) 0 2px,
    transparent 0 9px
  );
}
.container {
  background: #fff;
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  padding: 30px;
  border-radius: 5px;
  box-shadow: 0 3px 6px rgba(0, 0, 0, 0.16), 0 3px 6px rgba(0, 0, 0, 0.23);
  transition: all 0.3s cubic-bezier(0.25, 0.8, 0.25, 1);
}
.container:hover {
  box-shadow: 0 14px 28px rgba(0, 0, 0, 0.25), 0 10px 10px rgba(0, 0, 0, 0.22);
}
.btn {
  display: block;
  background: #444;
  color: #fff;
  padding: 10px 20px;
  margin: 15px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
  border: none;
  transition: 300ms;
}

.btn:focus {
  outline: none;
}
.btn-block {
  display: block;
  width: 100%;
}
</style>
