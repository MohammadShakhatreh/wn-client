<template>
  <v-layout class="mt-16 pt-16" column justify-center align-center>
    <v-card class="pa-5" min-width="400">
      <v-card-title>Log In</v-card-title>
      <v-form @submit.prevent="submit">
        <v-card-text>
          <v-text-field
            v-model="form.username"
            label="Username"
            type="text"
            prepend-inner-icon="mdi-account"
            outlined
          ></v-text-field>
          <v-text-field
            v-model="form.password"
            label="Password"
            type="password"
            prepend-inner-icon="mdi-lock"
            outlined
          ></v-text-field>
          <span class="text-caption"
            >You don't have an account?
            <nuxt-link to="/auth/signup">Sign Up</nuxt-link></span
          >
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn large type="submit">Log In</v-btn>
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
        username: '',
        password: '',
      },
    }
  },
  methods: {
    submit() {
      this.$auth
        .loginWith('local', {
          data: this.form,
        })
        .catch(() => this.$toast.error('Bad Credentials!'))
    },
  },
  head: {
    title: 'Log In',
  },
}
</script>
