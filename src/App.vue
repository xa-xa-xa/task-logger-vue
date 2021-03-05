<template>
  <div class="container">
<Header title="Task Logger" />
  </div>
</template>

<script>

import Header from './components/Header'
export default {
  name: 'App',
  components: {
    Header
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
