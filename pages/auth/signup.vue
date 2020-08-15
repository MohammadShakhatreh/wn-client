<template>
  <v-layout class="mt-16 pt-16" column justify-center align-center>
    <v-card class="pa-5" min-width="400">
      <v-card-title>Sign Up</v-card-title>
      <v-form @submit.prevent="submit">
        <v-card-text>
          <v-text-field
            v-model="form.name"
            label="Full name"
            type="text"
            outlined
          ></v-text-field>
          <v-text-field
            v-model="form.username"
            label="Username"
            type="text"
            outlined
          ></v-text-field>
          <v-text-field
            v-model="form.password"
            label="Password"
            type="password"
            outlined
          ></v-text-field>
          <span class="text-caption"
            >Already have an account?
            <nuxt-link to="/auth/login">Log In</nuxt-link></span
          >
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn large type="submit">Sign Up</v-btn>
        </v-card-actions>
      </v-form>
    </v-card>
  </v-layout>
</template>

<script>
export default {
  auth: 'guest',
  data() {
    return {
      form: {
        name: '',
        username: '',
        password: '',
      },
    }
  },

  methods: {
    submit() {
      // eslint-disable-next-line
      this.$axios
        .post('/users/', this.form)
        .then((data) => {
          this.$auth.loginWith('local', {
            data: {
              username: this.form.username,
              password: this.form.password,
            },
          })
        })
        .catch(() => this.$toast.error('Something went wrong!'))
    },
  },

  head: {
    title: 'Sign Up',
  },
}
</script>
