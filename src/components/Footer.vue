<template>
  <footer>
      <p>Copyright &copy; 2021 </p>
      <router-link v-show="onHomePage" to="/about">About</router-link>
  </footer>
</template>

<script>
export default {
    computed: {
         onHomePage() {
      return this.$route.path === '/';
    },   
    }
}
</script>

<style scoped>
a {
    color: #444;
    text-decoration: none;
    border-bottom: 4px solid transparent;
    transition: 300ms;
}
a:hover {
    color: #444;
    text-decoration: none;
    border-bottom: 4px solid rgba(0, 128, 0, 0.5);
    transition: 300ms;
}
footer {
    margin-top: 32px;
    text-align: center;
}

</style>

 