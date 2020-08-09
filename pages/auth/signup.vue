<template>
  <v-layout class="mt-16 pt-16" column justify-center align-center>
    <v-card class="pa-5" min-width="400">
      <v-card-title>Sign Up</v-card-title>
      <v-card-text>
        <v-form>
          <v-text-field label="Full name" type="text" outlined></v-text-field>
          <v-text-field label="Username" type="text" outlined></v-text-field>
          <v-text-field
            label="Password"
            type="password"
            outlined
          ></v-text-field>

          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn large @click="submit">Sign Up</v-btn>
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
        name: '',
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
