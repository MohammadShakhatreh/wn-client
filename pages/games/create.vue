<template>
  <v-layout class="mt-16 pt-16" column justify-center align-center>
    <v-card class="pa-5" min-width="400">
      <v-card-title>Create Game</v-card-title>
      <v-form @submit.prevent="submit">
        <v-card-text>
          <v-text-field
            v-model="form.name"
            label="Name"
            type="text"
            outlined
          ></v-text-field>
          <v-select
            v-model="form.mazeId"
            :items="mazes"
            item-text="name"
            item-value="id"
            label="Maze"
            outlined
          ></v-select>
          <v-text-field
            v-model="form.gold"
            label="Gold"
            type="number"
            outlined
          ></v-text-field>
          <v-text-field
            v-model="form.timeout"
            label="Timeout in minutes"
            type="number"
            outlined
          ></v-text-field>
          <v-text-field
            v-model="form.startsAfter"
            label="Starts after X minutes"
            type="number"
            outlined
          ></v-text-field>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn large type="submit">Create</v-btn>
        </v-card-actions>
      </v-form>
    </v-card>
  </v-layout>
</template>

<script>
export default {
  async asyncData({ $axios }) {
    const { data: mazes } = await $axios.get('/mazes')

    return {
      mazes,
      form: {
        name: null,
        mazeId: null,
        gold: 0,
        timeout: 0,
        startsAfter: 0,
      },
    }
  },

  methods: {
    async submit() {
      try {
        const { data: game } = await this.$axios.post('/games/', this.form)
        await this.$axios.post(`/games/${game.uuid}/join/`)
        this.$router.push(`/games/${game.uuid}/`)
      } catch (error) {
        // eslint-disable-next-line no-console
        console.log(error)
        this.$toast.error('Something went wrong!')
      }
    },
  },

  head: {
    title: 'Create Game',
  },
}
</script>

<style lang="scss"></style>
