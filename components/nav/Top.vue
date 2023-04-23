<template>
  <div class="nav">
    <NuxtLink class="nav-item" to="/">Strona domowa</NuxtLink>
    <NuxtLink class="nav-item" to="/about">O nas</NuxtLink>
    <NuxtLink class="nav-item" to="/gallery">Galeria</NuxtLink>
    <NuxtLink class="nav-item" to="/nasa">Nasa</NuxtLink>
  </div>
</template>

<script>

</script>
<style scoped>
.nav {
  display: flex;
  width: 100vw;
  color: white;
  height: 50px;
  background-color: #1b263b;
  justify-content: center;
  align-items: center;
}

.nav-item {
  padding: 0 10px;
  text-decoration: none;
  color: white;
}

.nuxt-link-exact-active, .nav-item:hover {
  color: #ffc300;
}
</style>
