<template>
  <v-layout class="mt-8" column>
    <v-row>
      <v-col>
        <h1 class="text-h2 text-center">{{ game.name }}</h1>
      </v-col>
    </v-row>
    <v-row class="pt-8">
      <v-col cols="3">
        <v-row>
          <v-col class="pt-0">
            <v-card>
              <v-list dense>
                <v-subheader>Status</v-subheader>
                <v-list-item>
                  <v-list-item-content>
                    <v-list-item-title>
                      Username: {{ status.username }}
                    </v-list-item-title>
                  </v-list-item-content>
                </v-list-item>
                <v-list-item>
                  <v-list-item-content>
                    <v-list-item-title>
                      Mode: {{ status.mode.toLowerCase() }}
                    </v-list-item-title>
                  </v-list-item-content>
                </v-list-item>
                <v-list-item>
                  <v-list-item-content>
                    <v-list-item-title>
                      Gold: {{ status.gold }}
                    </v-list-item-title>
                  </v-list-item-content>
                </v-list-item>
                <v-list-item>
                  <v-list-item-content>
                    <v-list-item-title>
                      Direction: {{ status.direction.toLowerCase() }}
                    </v-list-item-title>
                  </v-list-item-content>
                </v-list-item>
                <v-list-item>
                  <v-list-item-content>
                    <v-list-item-title>
                      Location: {{ status.location }}
                    </v-list-item-title>
                  </v-list-item-content>
                </v-list-item>
                <v-list-item>
                  <v-list-item-content>
                    <v-list-item-title>
                      Items
                    </v-list-item-title>
                    <v-list dense>
                      <v-list-item v-for="item in status.items" :key="item">
                        <v-list-item-content>
                          <v-list-item-title> - {{ item }} </v-list-item-title>
                        </v-list-item-content>
                      </v-list-item>
                    </v-list>
                  </v-list-item-content>
                </v-list-item>
              </v-list>
            </v-card>
          </v-col>
        </v-row>
        <v-row>
          <v-col>
            <v-card>
              <v-list dense>
                <v-subheader>Players ({{ players.length }})</v-subheader>
                <v-list-item v-for="player in players" :key="player.username">
                  <v-list-item-content>
                    <v-list-item-title>{{ player.username }}</v-list-item-title>
                  </v-list-item-content>
                </v-list-item>
              </v-list>
            </v-card>
          </v-col>
        </v-row>
      </v-col>
      <v-col cols="5">
        <v-row>
          <v-col class="pt-0">
            <v-text-field
              v-model="prompt"
              placeholder="Command Prompt"
              hint="Type the command and hit enter."
              solo
              autofocus
              @keypress.enter="execute"
            ></v-text-field>
          </v-col>
        </v-row>
        <v-row>
          <v-col>
            <v-card>
              <v-card-title>Command Result:</v-card-title>
              <v-card-text>
                <pre>{{ result }}</pre>
              </v-card-text>
            </v-card>
          </v-col>
        </v-row>
      </v-col>
      <v-col cols="4">
        <v-card>
          <v-list dense three-line>
            <v-subheader>Commands</v-subheader>
            <v-list-item v-for="command in commands" :key="command.name">
              <v-list-item-content>
                <v-list-item-title>
                  {{ `${command.name} ${command.arguments}` }}
                </v-list-item-title>
                <v-list-item-subtitle>
                  {{ command.description }}
                </v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>
          </v-list>
        </v-card>
      </v-col>
    </v-row>
  </v-layout>
</template>

<script>
export default {
  async asyncData({ params, $axios }) {
    const { data: game } = await $axios.get(`/games/${params.uuid}/`)
    const { data: status } = await $axios.get(`/games/${params.uuid}/status`)

    const { data: commands } = await $axios.get(
      `/games/${params.uuid}/commands`
    )

    const { data: players } = await $axios.get(`/games/${params.uuid}/players`)

    return {
      game,
      status,
      players,
      commands,
      prompt: '',
      result: '',
    }
  },

  methods: {
    async execute() {
      if (!this.prompt) return

      try {
        const uuid = this.game.uuid

        const {
          data: { result },
        } = await this.$axios.post(`/games/${uuid}/execute`, {
          line: this.prompt,
        })
        this.result = result

        const { data: game } = await this.$axios.get(`/games/${uuid}/`)
        this.game = game

        const { data: status } = await this.$axios.get(`/games/${uuid}/status`)
        this.status = status

        const { data: commands } = await this.$axios.get(
          `/games/${uuid}/commands`
        )
        this.commands = commands

        const { data: players } = await this.$axios.get(
          `/games/${uuid}/players`
        )
        this.players = players
      } catch (error) {
        this.$toast.error('Something went wrong!!')
      }
    },
  },

  head() {
    return {
      title: this.game.name,
    }
  },
}
</script>

<style lang="scss"></style>
