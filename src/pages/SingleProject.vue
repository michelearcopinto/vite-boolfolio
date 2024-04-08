<script>
import { store } from "../store";
import axios from "axios";

export default {
  name: "SinglePost",
  data() {
    return {
      project: null,
      store,
    };
  },
  methods: {
    getSingleProject() {
      axios
        .get(`${store.apiBaseUrl}/api/test/${this.$route.params.slug}`)
        .then((result) => {
          if (result.data.success) {
            this.project = result.data.project;
            console.log(this.project);
          } else {
            this.$router.push({ name: "not-found" });
          }
        });
    },
  },
  mounted() {
    this.getSingleProject();
  },
};
</script>

<template>
  <div v-if="project" class="p-3">
    <h2 class="card-title">
      {{ project.title }}
    </h2>
    <figure v-show="project.cover_image" class="mt-3">
      <img
        :src="`${store.apiBaseUrl}/storage/${project.cover_image}`"
        :alt="project.slug"
      />
    </figure>
    <ul>
      <li>
        slug: <strong>{{ project.slug }}</strong>
      </li>
      <li v-if="project.category">
        category:
        <strong>{{ project.category.name }}</strong>
      </li>
      <li v-else>
        category:
        <strong>Nessuna</strong>
      </li>
      <li>
        tags:
        <span
          v-if="project.tags.length > 0"
          v-for="(element, index) in project.tags"
          class="badge rounded-pill text-bg-primary me-1"
          >{{ element.name }}</span
        >
        <span v-else><strong>Nessuno</strong></span>
      </li>
    </ul>
    <p class="card-text">{{ project.description }}</p>
  </div>
  <div
    v-else
    class="d-flex justify-content-center align-items-center"
    style="min-height: 100vh; background-color: #f8f9fa"
  >
    <span
      class="spinner-border text-primary me-2"
      role="status"
      aria-hidden="true"
    ></span>
    <span>Caricamento in corso...</span>
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

ol,
ul {
  padding-left: 1rem;
}

img {
  width: 450px;
}
</style>
