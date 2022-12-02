<template>
  <nav>
    <router-link to="/"> Projects /</router-link>
    <router-link :to="{ name: 'addProject' }"> Add Project </router-link>
  </nav>
</template>

<script>
export default {};
</script>

<style>
nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
  margin-right: 10px;
  text-decoration: none;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>