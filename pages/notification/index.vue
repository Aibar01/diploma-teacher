<template>
  <v-container fluid>
    <v-row v-if="!is_active" class="pt-5 pl-5">
      <v-col>No notifications yet</v-col>
    </v-row>
    <v-row>
      <v-col cols="12">
        <v-card max-width="500" elevation="0">
          <v-spacer></v-spacer>
          <v-card-text>
            <v-btn color="#10AFA7" text class="text-capitalize">
              Тазалау
            </v-btn>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
    <v-row class="pl-5">
      <v-col v-for="(item, index) in data" :key="index" cols="12">
        <v-card max-width="500" outlined>
          <v-card-text>
            <p class="text-h6 text--primary">{{ item.title }}</p>
            <div class="text--primary">
              {{ item.content }}
            </div>
          </v-card-text>
          <v-card-text style="display: flex" class="caption">
            <div>
              {{ item.date }}
            </div>
            <div
              v-if="item.type == 'course'"
              style="color: #10afa7"
              class="pl-5 font-weight-bold"
            >
              Go to course
            </div>
            <div
              v-else-if="item.type == 'homework'"
              style="color: #10afa7"
              class="pl-5 font-weight-bold"
            >
              See homework
            </div>
          </v-card-text>

          <v-expand-transition>
            <v-card
              v-if="reveal"
              class="transition-fast-in-fast-out v-card--reveal"
              style="height: 100%"
            >
              <v-card-text class="pb-0">
                <p class="display-1 text--primary">Origin</p>
                <p>
                  late 16th century (as a noun denoting a place where alms were
                  distributed): from medieval Latin eleemosynarius, from late
                  Latin eleemosyna ‘alms’, from Greek eleēmosunē ‘compassion’
                </p>
              </v-card-text>
              <v-card-actions class="pt-0">
                <v-btn text color="teal accent-4" @click="reveal = false">
                  Close
                </v-btn>
              </v-card-actions>
            </v-card>
          </v-expand-transition>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  layout(context) {
    return 'notification'
  },
  data() {
    return {
      is_active: true,
      data: [
        {
          title: 'You were added to private class “Learn Scratch with Chris”',
          content:
            'You were added to class “Learn Scratch with Chris” by your teacher Chris from your organization.',
          date: '12 Mar 2021 at 12:01',
          type: 'course',
        },
        {
          title: 'Welcome to our App!',
          content:
            'We are happy to see you as a part of our service and comunity. Enjoy our app, learn and study new knowledges.',
          date: '12 Mar 2021 at 12:01',
          type: 'notification',
        },
      ],
    }
  },
}
</script>

<style scoped>
.link {
  color: #10afa7 !important;
}
</style>
