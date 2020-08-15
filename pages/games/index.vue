<template>
  <v-layout class="mt-16" column justify-center align-center>
    <v-row>
      <v-col>
        <h1 class="text-h1">Games</h1>
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <span>Welcome, {{ $auth.user.name }}</span>
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <v-btn nuxt to="/games/create">New Game</v-btn>
      </v-col>
      <v-col>
        <v-btn @click="$auth.logout('local')">Log out</v-btn>
      </v-col>
    </v-row>
    <v-row>
      <v-divider class="my-4" style="width: 550px;"></v-divider>
    </v-row>
    <v-row>
      <v-col v-if="games && games.length > 0">
        <v-row v-for="game in games" :key="game.uuid">
          <v-col>
            <game-item :game="game" width="550" />
          </v-col>
        </v-row>
      </v-col>
      <v-col v-else>
        <span>There is no games to join, try creating new game.</span>
      </v-col>
    </v-row>
  </v-layout>
</template>

<script>
import GameItem from '@/components/GameItem'
export default {
  components: {
    GameItem,
  },

  async asyncData({ $axios }) {
    const { data } = await $axios.get('/games/')
    return { games: data }
  },

  head: {
    title: 'Games',
  },
}
</script>

<style lang="scss"></style>
