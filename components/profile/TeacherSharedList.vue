<template>
  <v-card elevation="0" max-width="975" class="ml-auto mt-5">
    <v-container>
      <v-row>
        <v-col v-for="item in items.results" :key="item.id" cols="12">
          <v-card elevation="0">
            <div class="d-flex flex-no-wrap justify-space-between">
              <div>
                <v-list-item two-line>
                  <v-list-item-avatar rounded>
                    <img v-if="$auth.user.avatar" :src="$auth.user.avatar" />
                    <img
                      v-else
                      src="https://randomuser.me/api/portraits/women/81.jpg"
                    />
                  </v-list-item-avatar>

                  <v-list-item-action-text>
                    <v-list-item-title
                      >{{ $auth.user.first_name }}
                      {{ $auth.user.last_name }}</v-list-item-title
                    >
                  </v-list-item-action-text>

                  <v-list-item-action>
                    <v-list-item-title class="grey--text">
                      Programming teacher
                    </v-list-item-title>
                  </v-list-item-action>
                </v-list-item>

                <v-card-title class="headline">
                  {{ item.title }}
                </v-card-title>

                <v-card-subtitle>
                  {{ item.text }}
                </v-card-subtitle>

                <v-card-actions>
                  <v-card-subtitle class="pt-4 pb-6">
                    <v-icon small class="pb-1">
                      mdi-calendar-blank-outline
                    </v-icon>
                    {{
                      $moment(new Date(+item.created_date * 1000)).format(
                        'MMM D, YYYY'
                      )
                    }}
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
export default {
  data() {
    return {
      items: [],
    }
  },
  async fetch() {
    try {
      this.items = await this.$axios.$get('news/news/')
    } catch (err) {
      // eslint-disable-next-line no-console
      console.log(err)
    }
  },
}
</script>
