<script>
import ContactForm from "../components/ContactForm.vue";

export default {
  name: "ContactUs",
  components: {
    ContactForm,
  },
};
</script>

<template>
  <div class="container">
    <div class="row">
      <div class="col-12">
        <h1>Contatti</h1>
        <ContactForm />
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
@use "../styles/partials/variables" as *;
@use "../styles/partials/mixins" as *;
</style>
