<template>
  <v-layout class="mt-16 pt-16" column justify-center align-center>
    <v-row>
      <v-col>
        <h1 class="text-center text-h1">World Navigator</h1>
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <h2 class="text-center text-subtitle-1">
          Multi-player text adventure game.
        </h2>
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <v-btn x-large nuxt to="/auth/login">Log In</v-btn>
      </v-col>
      <v-col>
        <v-btn x-large outlined nuxt to="/auth/signup">Sign Up</v-btn>
      </v-col>
    </v-row>
  </v-layout>
</template>

<script>
export default {
  auth: false,
}
</script>
