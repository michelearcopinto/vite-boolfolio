<script>
import AppHeader from "./components/AppHeader.vue";

export default {
  components: {
    AppHeader,
  },
  data() {
    return {};
  },
  mounted() {},
  methods: {},
};
</script>

<template>
  <AppHeader />

  <router-view></router-view>
</template>

<style lang="scss">
@use "./styles/general.scss";
</style>
