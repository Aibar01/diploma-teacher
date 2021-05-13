<template>
  <v-card class="pl-5 pt-5" elevation="0" max-width="700">
    <v-form @submit.prevent="aboutClass">
      <v-row>
        <v-col class="font-weight-bold text-uppercase">About course</v-col>
        <v-col>
          <v-textarea
            v-model="item.about_course"
            outlined
            name="input-7-4"
            label="Enter something"
            :value="item.about_course"
          ></v-textarea>
        </v-col>
      </v-row>
      <v-row>
        <v-col class="font-weight-bold text-uppercase">Syllabus</v-col>
        <v-col>
          <v-combobox
            v-model="item.syllabus"
            label="Syllabus"
            multiple
            chips
          ></v-combobox>
        </v-col>
      </v-row>
      <v-row>
        <v-col class="font-weight-bold text-uppercase">Teacher</v-col>
        <v-col>
          <v-card elevation="0" max-width="800">
            <v-card-title class="pt-0">
              <v-list-item class="pl-0 grow">
                <v-list-item-avatar color="#10AFA7">
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
      <v-card-actions>
        <v-btn class="text-capitalize" color="#10AFA7" dark type="submit">
          Save
        </v-btn>
      </v-card-actions>
    </v-form>
  </v-card>
</template>

<script>
export default {
  layout: 'class',
  middleware: 'auth',
  async asyncData({ $axios, params }) {
    try {
      const item = await $axios.$get(`classes/class/${params.id}/`)
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
  methods: {
    async aboutClass() {
      try {
        await this.$axios.$patch(`classes/class/${this.$route.params.id}/`, {
          syllabus: this.item.syllabus,
          about_course: this.item.about_course,
        })
      } catch (err) {
        // eslint-disable-next-line no-console
        console.log(err)
      }
    },
  },
}
</script>
