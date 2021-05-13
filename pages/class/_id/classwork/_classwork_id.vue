<template>
  <v-container fluid>
    <v-row class="pt-5 pl-5">
      <v-col cols="12">
        <v-card outlined max-width="500">
          <v-card-title class="py-0">
            <v-list-item class="pl-0 pr-0 grow">
              <v-list-item-avatar color="#10AFA7">
                <span class="white--text headline">
                  <v-icon dark>mdi-notebook</v-icon>
                </span>
              </v-list-item-avatar>

              <v-list-item-content>
                <div style="display: flex">
                  <v-list-item-title>{{ item.title }}</v-list-item-title>
                  <v-btn icon color="#C4C4C4">
                    <v-icon>mdi-dots-horizontal</v-icon>
                  </v-btn>
                </div>
                <v-list-item-subtitle>{{
                  $moment(new Date(+item.created_at * 1000)).format(
                    'D MMM YYYY, h:mm'
                  )
                }}</v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>
          </v-card-title>
          <v-card-text v-if="item.uploaded_file">
            <div class="d-flex">
              <v-card class="mb-4" outlined>
                <div class="d-flex">
                  <v-avatar width="100" height="75" tile>
                    <v-icon x-large class="pt-2"> mdi-file </v-icon>
                  </v-avatar>
                  <div>
                    <v-card-title class="text-h6 pl-0">{{
                      item.uploaded_file.substring(
                        item.uploaded_file.lastIndexOf('/') + 1
                      )
                    }}</v-card-title>

                    <v-card-subtitle class="pl-0"
                      >{{ item.file_size }} MB</v-card-subtitle
                    >
                  </div>
                </div>
              </v-card>
            </div>
          </v-card-text>
          <v-card-text v-if="item.due_date" class="font-weight-bold">
            Due to
            {{
              $moment(new Date(+item.due_date * 1000)).format(
                'D MMM YYYY, h:mm'
              )
            }}
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  layout: 'classwork',
  middleware: 'auth',
  async asyncData({ $axios, params }) {
    try {
      const item = await $axios.$get(
        `classes/classworkes/${params.classwork_id}/`
      )

      return { item }
    } catch (err) {
      return { item: {} }
    }
  },
  data() {
    return {
      item: {},
    }
  },
}
</script>

<style scoped>
.v-input__slot {
  margin-bottom: 0;
}
</style>
