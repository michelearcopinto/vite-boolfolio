<script>
import ProjectCard from "../components/ProjectCard.vue";
import { store } from "../store";
import axios from "axios";

export default {
  components: {
    ProjectCard,
  },
  data() {
    return {
      arrayProjects: [],
      currentPage: "",
      lastPage: "",
      store,
    };
  },
  mounted() {
    this.getProjects(1);
  },
  methods: {
    getProjects(postApiPage) {
      axios
        .get(
          `${store.apiBaseUrl}/api/test`,

          {
            params: {
              page: postApiPage,
            },
          }
        )
        .then((result) => {
          this.arrayProjects = result.data.projects.data;
          this.currentPage = result.data.projects.current_page;
          this.lastPage = result.data.projects.last_page;

          console.log(this.currentPage, this.lastPage);
        });
    },
  },
};
</script>

<template>
  <div v-if="arrayProjects.length > 0" class="container mt-3">
    <h1 class="mb-4">Lista progetti</h1>
    <div class="row">
      <ProjectCard
        v-for="(element, index) in arrayProjects"
        :key="index"
        :propElement="element"
      />
    </div>
    <nav aria-label="Page navigation example">
      <ul class="pagination mx-auto">
        <li class="page-item">
          <button
            class="page-link"
            :class="{ disabled: currentPage === 1 }"
            @click="getProjects(currentPage - 1)"
          >
            Previous
          </button>
        </li>

        <li class="page-item" v-for="(element, index) in lastPage" :key="index">
          <button
            class="page-link"
            :class="{ disabled: currentPage === element }"
            @click="getProjects(element)"
          >
            {{ element }}
          </button>
        </li>

        <li class="page-item">
          <button
            class="page-link"
            :class="{ disabled: currentPage === lastPage }"
            @click="getProjects(currentPage + 1)"
          >
            Next
          </button>
        </li>
      </ul>
    </nav>
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
  text-transform: uppercase;
  color: black;
  margin-inline: 20px;
}
</style>
