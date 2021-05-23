<template>
  <v-container fluid>
    <v-row class="pl-4">
      <v-col class="pb-0">
        <div class="text-uppercase">Мұғалім</div>
      </v-col>
    </v-row>
    <v-row>
      <v-col class="py-0">
        <v-card elevation="0" max-width="500">
          <v-card-title class="pb-0">
            <v-list-item class="pl-0 grow">
              <v-list-item-avatar>
                <img
                  v-if="$auth.user.avatar"
                  alt="Avatar"
                  :src="$auth.user.avatar"
                />
                <img
                  v-else
                  alt="Avatar"
                  src="https://avatars0.githubusercontent.com/u/9064066?v=4&s=460"
                />
              </v-list-item-avatar>

              <v-list-item-content>
                <v-list-item-title>
                  {{ $auth.user.first_name }} {{ $auth.user.last_name }}
                </v-list-item-title>
              </v-list-item-content>
            </v-list-item>
          </v-card-title>
        </v-card>
      </v-col>
    </v-row>
    <v-row class="pl-4">
      <v-col>
        <div class="text-uppercase">Оқушылар</div>
      </v-col>
    </v-row>
    <v-row>
      <v-col
        v-for="item in items.results"
        :key="item.id"
        cols="12"
        class="py-0"
      >
        <v-card elevation="0" max-width="500">
          <v-card-title class="pb-0">
            <v-list-item class="pl-0 grow">
              <v-list-item-avatar color="#10AFA7">
                <img v-if="item.avatar" alt="Avatar" :src="item.avatar" />
                <img
                  v-else
                  alt="Avatar"
                  src="https://avatars0.githubusercontent.com/u/9064066?v=4&s=460"
                />
              </v-list-item-avatar>

              <v-list-item-content>
                <v-list-item-title>
                  {{ item.first_name }} {{ item.last_name }}
                </v-list-item-title>
              </v-list-item-content>
            </v-list-item>
          </v-card-title>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  layout: 'class',
  middleware: 'auth',
  async asyncData({ $axios, params }) {
    try {
      const items = await $axios.$get(`classes/students/${params.id}/`)
      return {
        items,
      }
    } catch (err) {
      return { items: [] }
    }
  },
  data() {
    return {
      items: [],
    }
  },
}
</script>
