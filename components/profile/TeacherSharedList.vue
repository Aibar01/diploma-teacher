<template>
  <v-card elevation="0" max-width="975" class="ml-auto mt-5">
    <v-container>
      <v-row>
        <v-col v-for="(item, i) in items" :key="i" cols="12">
          <v-card elevation="0">
            <div class="d-flex flex-no-wrap justify-space-between">
              <div>
                <Avatar />
                <v-card-title class="headline">
                  {{ item.title }}
                </v-card-title>

                <v-card-subtitle>
                  We are about to start the new year 2021 and the last year has
                  been quite different and influenced the way we designed a lot.
                  But let’s not talk about the last year.
                </v-card-subtitle>

                <v-card-actions>
                  <v-card-subtitle class="pt-4 pb-6">
                    <v-icon small class="pb-1">
                      mdi-calendar-blank-outline
                    </v-icon>
                    Sep 8, 2020
                  </v-card-subtitle>

                  <v-spacer></v-spacer>

                  <v-card-subtitle class="pt-4 pb-6">
                    <v-icon class="pb-1"> mdi-heart-outline </v-icon>
                  </v-card-subtitle>
                </v-card-actions>
              </div>

              <v-avatar
                class="my-auto"
                max-height="180"
                max-width="262"
                size="262"
                rounded
              >
                <v-img :src="item.src"></v-img>
              </v-avatar>
            </div>
            <v-divider></v-divider>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </v-card>
</template>

<script>
import Avatar from '../search/Avatar'

export default {
  components: {
    Avatar,
  },
  data: () => ({
    items: [
      {
        src: 'https://cdn.vuetifyjs.com/images/cards/foster.jpg',
        title: 'Here will be One lined Post title 2021',
        teacher: 'Jane Smith',
      },
      {
        src: 'https://cdn.vuetifyjs.com/images/cards/halcyon.png',
        title: 'Here will be One lined Post title 2021',
        teacher: 'Jane Smith',
      },
    ],
  }),
}
</script>
