<script>
import { store } from "../store";
import axios from "axios";

export default {
  name: "ContactForm",
  data() {
    return {
      store,
      name: "",
      email: "",
      message: "",
      errors: {},
      success: false,
    };
  },
  methods: {
    sendForm() {
      const data = {
        name: this.name,
        email: this.email,
        message: this.message,
      };

      this.errors = {};

      axios
        .post(`${this.store.apiBaseUrl}/api/contacts`, data)
        .then((response) => {
          this.success = response.data.success;
          if (!this.success) {
            this.errors = response.data.errors;
          } else {
            this.name = "";
            this.email = "";
            this.message = "";
          }
        });
    },
  },
  mounted() {},
};
</script>

<template>
  <div>
    <h2>Contact form</h2>

    <div class="alert alert-success" v-if="success">
      Messaggio inviato correttamente
    </div>

    <div class="">
      <form action="" @submit.prevent="sendForm()">
        <div class="mb-3">
          <input
            type="text"
            class="form-control"
            :class="{ 'is-invalid': errors.name }"
            name="name"
            placeholder="Inserisci il tuo nome"
            v-model="name"
          />

          <p
            v-for="(error, index) in error?.name"
            :key="`message-errors-${index}`"
            class="invalid-feedback"
          >
            {{ error }}
          </p>
        </div>

        <div class="mb-3">
          <input
            type="email"
            class="form-control"
            :class="{ 'is-invalid': errors.email }"
            name="email"
            placeholder="Inserisci una mail valida"
            v-model="email"
          />

          <p
            v-for="(error, index) in error?.email"
            :key="`message-errors-${index}`"
            class="invalid-feedback"
          >
            {{ error }}
          </p>
        </div>

        <div class="mb-3">
          <textarea
            name="message"
            :class="{ 'is-invalid': errors.message }"
            id="message"
            cols="30"
            rows="10"
            v-model="message"
          ></textarea>

          <p
            v-for="(error, index) in error?.message"
            :key="`message-errors-${index}`"
            class="invalid-feedback"
          >
            {{ error }}
          </p>
        </div>

        <button class="btn btn-primary" type="submit">Send</button>
      </form>
    </div>
  </div>
</template>

<style lang="scss" scoped>
@use "../styles/partials/variables" as *;
@use "../styles/partials/mixins" as *;
</style>
