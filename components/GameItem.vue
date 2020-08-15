<template>
  <v-card :width="width">
    <v-container class="py-0">
      <v-row>
        <v-col cols="10">
          <v-row>
            <v-card-title class="py-0">{{ game.name }}</v-card-title>
          </v-row>
          <v-row>
            <v-card-subtitle class="py-0">
              Players: {{ game.playerCount }} | Starts at: {{ startedAt }}
            </v-card-subtitle>
          </v-row>
        </v-col>
        <v-col cols="2">
          <v-card-actions>
            <v-btn @click="join">Join</v-btn>
          </v-card-actions>
        </v-col>
      </v-row>
    </v-container>
  </v-card>
</template>

<script>
import moment from 'moment'

export default {
  props: {
    width: {
      type: String,
      default: undefined,
    },
    game: {
      type: Object,
      reqired: true,
      default: null,
    },
  },

  computed: {
    startedAt: ({ game }) => moment(game.startedAt).format('h:mm:ss'),
  },

  methods: {
    join() {
      const { uuid } = this.game
      this.$axios
        .post(`/games/${uuid}/join`)
        .then(() => this.$router.push(`/games/${uuid}/`))
        .catch(() => this.$toast.error('Something went wrong!'))
    },
  },
}
</script>
