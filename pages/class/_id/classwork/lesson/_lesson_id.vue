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
                  <v-list-item-title>{{ data.title }}</v-list-item-title>
                  <v-btn icon color="#C4C4C4">
                    <v-icon>mdi-dots-horizontal</v-icon>
                  </v-btn>
                </div>
                <v-list-item-subtitle>{{ data.date }}</v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>
          </v-card-title>
          <v-card-text>
            <div v-for="i in 3" :key="i" class="d-flex">
              <v-card class="mb-4" outlined>
                <div class="d-flex">
                  <v-avatar width="100" height="75" tile>
                    <v-icon x-large class="pt-2"> mdi-file </v-icon>
                  </v-avatar>
                  <div>
                    <v-card-title class="text-h6 pl-0">Main book</v-card-title>

                    <v-card-subtitle class="pl-0">9.3 MB</v-card-subtitle>
                  </div>
                </div>
              </v-card>
            </div>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  layout: 'class',
  middleware: 'auth',
  data() {
    return {
      data: {
        title: 'Material',
        content:
          'Hello everyone! I am glad to welcome you to this course based on Scratch. I am adding every student mannually, if you have friends who didn’t join this class till 18.03.2021 ask them to email me directly. Thank you!',
        date: '12 Mar 2021 at 12:01',
        type: 'notfication',
      },
    }
  },
}
</script>

<style scoped>
.v-input__slot {
  margin-bottom: 0;
}
</style>
