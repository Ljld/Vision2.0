<template>
  <div class="containerd">
    <div class="navbar">
      <div class="logo">
        <h2>Vision 2.0</h2>
      </div>
      <div class="menu">
        <p>
          <NuxtLink to="/corporate">Corporate</NuxtLink>
        </p>
        <p>Dark mode</p>
        <p>
          <NuxtLink to="/">Gradient</NuxtLink>
        </p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Navbar"
}
</script>

<style scoped>
.containerd {
  background-color: #121212;
}
.navbar {
  background-color: #121212;

  color: white;
  display: flex;
  justify-content: space-between;
  padding: 2em 0;
  margin: 0 10em;
}

.menu {
  display: flex;
}

.menu > p {
  padding: 0 1em;
}
</style>
