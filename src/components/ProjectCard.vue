<script>
// import

export default {
  name: "ProjectCard",
  props: ["propElement"],
};
</script>

<template>
  <div class="col-4 project-container">
    <div class="card text-start p-3 project-card">
      <figure v-show="propElement.cover_image">
        <img
          class="card-img-top"
          :src="propElement.cover_image"
          :alt="propElement.slug"
        />
      </figure>
      <div class="card-body">
        <h4 class="card-title">{{ propElement.title }}</h4>
        <ul>
          <li>
            slug: <strong>{{ propElement.slug }}</strong>
          </li>
          <li v-if="propElement.category">
            category:
            <strong>{{ propElement.category.name }}</strong>
          </li>
          <li v-else>
            category:
            <strong>Nessuna</strong>
          </li>
          <li>
            tags:
            <span
              v-if="propElement.tags.length > 0"
              v-for="(element, index) in propElement.tags"
              class="badge rounded-pill text-bg-primary me-1"
              >{{ element.name }}</span
            >
            <span v-else><strong>Nessuno</strong></span>
          </li>
        </ul>
        <p class="card-text">{{ propElement.description }}</p>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
@use "../styles/partials/variables" as *;
@use "../styles/partials/mixins" as *;

h1 {
  color: $font-color-second;
  @include main-font-start;
}

li {
  list-style-type: disc;
}

.project-container {
  height: 450px;

  .project-card {
    height: 100%;
    overflow: auto;
  }
}

ol,
ul {
  padding-left: 1rem;
}
</style>
