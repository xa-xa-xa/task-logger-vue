<template>
  <div>
    <h1>About:</h1>  <h3>
    Version 1.0.0
    <p>
      <router-link to="/">Back</router-link>
    </p>
  </h3>

  </div>
</template>

<script>
export default {
  name: 'About',
};
</script>

<style>
a {
  text-decoration: none;
  text-align: center;
  color: #444;
}
p {
  margin-top: 1rem;
}
p> a {
    border-bottom: 4px solid transparent;
      transition: 300ms;

}
p > a:hover {
  transition: 200ms;
  border-bottom: 4px solid rgba(0, 128, 0, 0.5);

}


h3, h1 {
  text-align: center;
}
</style>
