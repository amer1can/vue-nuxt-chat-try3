<template>
  <v-row
    no-gutters
    align="center"
    justify="center"
  >
    <v-col cols="auto">
      <v-card
        min-width="290"
        color="grey"
      >
        <v-snackbar v-model="snackbar" :timeout="3000" bottom>
          {{ message }}
          <v-btn dark text @click="snackbar = false">Close</v-btn>
        </v-snackbar>

        <v-card-title>
          <h2>Login</h2>
        </v-card-title>
        <v-card-text>
          <v-form
            ref="form"
            v-model="isValid"
            lazy-validation
            @submit.prevent="submit"
          >
            <v-text-field
              v-model="user.name"
              :counter="16"
              :rules="nameRules"
              label="Name"
              required
            />
            <v-text-field
              v-model="user.room"
              :counter="16"
              :rules="roomRules"
              label="Enter the room"
              required
            />
            <v-btn
              :disabled="!isValid"
              color="primary"
              class="mt-3"
              type="submit"
            >
              Submit
            </v-btn>
          </v-form>
        </v-card-text>
      </v-card>
    </v-col>
  </v-row>
</template>
<script>

import { mapActions } from "vuex";

export default {
  name: 'IndexPage',
  layout: 'login',
  data: () => ({
    isValid: true,
    user: {
      name: "",
      room: "",
    },
    nameRules: [
      v => !!v || "Name is required",
      v => (v && v.length <= 16) || "Name must be less than 16 characters",
    ],
    roomRules: [
      v => !!v || "Enter the room",
      v => (v && v.length <= 16) || "Room must be less than 16 characters",
    ],
    snackbar: false,
  }),
  computed: {
    message() {
      const { message } = this.$route.query;

      if (message === "noUser") {
        return "Enter your name and room";
      } else if (message === "leftChat") {
        return "You leaved chat";
      }
      return 'loading successfully'
    },
  },
  mounted() {
    this.snackbar = !!this.message;
  },
  head: {
    title: "My Nuxt Chat",
  },
  methods: {
    ...mapActions([
      'createUser'
    ]),
    submit() {
      if (this.$refs.form.validate()) {
        this.createUser(this.user)
        this.$router.push('/chat')
      }
    }
  }
}
</script>
