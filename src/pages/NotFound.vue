<script>
// import

export default {
  name: "NotFound",
};
</script>

<template>
  <div
    class="d-flex flex-column justify-content-center align-items-center vh-100"
  >
    <h1 class="display-1 text-danger">Errore 404</h1>
    <p class="lead">La pagina che stai cercando non è stata trovata.</p>
  </div>
</template>

<style lang="scss" scoped>
@use "../styles/partials/variables" as *;
@use "../styles/partials/mixins" as *;
</style>
