<template>
  <v-layout class="mt-16 pt-16" column justify-center align-center>
    <v-card class="pa-5" min-width="400">
      <v-card-title>Log In</v-card-title>
      <v-card-text>
        <v-form>
          <v-text-field
            label="Username"
            type="text"
            prepend-inner-icon="mdi-account"
            outlined
          ></v-text-field>
          <v-text-field
            label="Password"
            type="password"
            prepend-inner-icon="mdi-lock"
            outlined
          ></v-text-field>

          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn large @click="submit">Log In</v-btn>
          </v-card-actions>
        </v-form>
      </v-card-text>
    </v-card>
  </v-layout>
</template>

<script>
export default {
  data() {
    return {
      form: {
        username: '',
        password: '',
      },
    }
  },

  methods: {
    submit() {},
  },
}
</script>
