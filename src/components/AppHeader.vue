<script>
// import

export default {
  name: "AppHeader",
};
</script>

<template>
  <nav class="navbar navbar-expand-lg bg-body-tertiary">
    <div class="container-fluid">
      <h1>Boolpress</h1>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarNav"
        aria-controls="navbarNav"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav">
          <li class="nav-item">
            <router-link
              :to="{ name: 'home' }"
              class="nav-link"
              aria-current="page"
              href="#"
            >
              Home
            </router-link>
          </li>
          <li class="nav-item">
            <router-link
              :to="{ name: 'blog' }"
              class="nav-link"
              aria-current="page"
              href="#"
            >
              Blog
            </router-link>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>

<style lang="scss" scoped>
@use "../styles/partials/variables" as *;
@use "../styles/partials/mixins" as *;

h1 {
  text-transform: uppercase;
  color: black;
  margin-inline: 20px;
}
</style>
