<script>
import ProjectCard from "./components/ProjectCard.vue";
import { store } from "./store";
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
    };
  },
  mounted() {
    this.getProjects(1);
  },
  methods: {
    getProjects(postApiPage) {
      axios
        .get(
          "http://127.0.0.1:8000/api/test",

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
  <h1>Stampa projects</h1>
  <div class="container mt-5">
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
</template>

<style lang="scss">
@use "./styles/general.scss";

h2 {
  font-size: 120px;
  color: aquamarine;
}

h3 {
  font-size: 80px;
  color: blueviolet;
}
</style>
