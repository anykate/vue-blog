<template>
  <header>
    <h1>Blog</h1>
    <nav>
      <router-link :to="{ name: 'Home' }" class="nav-home"> Home </router-link>
      <router-link :to="{ name: 'Create' }" class="nav-create">
        Create
      </router-link>
    </nav>
  </header>
</template>

<script>
export default {
  name: 'Navbar'
}
</script>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  max-width: 1200px;
  margin: 0 auto;
  padding: 10px;
  /* background-color: red; */
}
header h1 {
  color: blueviolet;
  font-size: 48px;
}
nav a {
  color: blueviolet;
  text-decoration: none;
  margin-left: 10px;
}
nav a.router-link-active {
  color: black;
  font-weight: bold;
}
</style>