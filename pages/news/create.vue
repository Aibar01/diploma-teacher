<template>
  <div class="mt-10">
    <v-card elevation="0" max-width="900" class="mx-auto">
      <v-card-title class="pb-0">
        <v-list-item class="mb-5">
          <v-spacer></v-spacer>
          <v-btn icon class="ml-auto"><v-icon x-large>mdi-close</v-icon></v-btn>
        </v-list-item>
        <v-list-item class="pl-0 grow">
          <v-list-item-avatar color="#10AFA7">
            <img alt="Avatar" :src="$auth.user.avatar" />
          </v-list-item-avatar>

          <v-list-item-content>
            <div class="d-flex">
              <div>
                <v-list-item-title>
                  {{ $auth.user.first_name }} {{ $auth.user.last_name }}
                </v-list-item-title>
                <v-list-item-subtitle> Writing new </v-list-item-subtitle>
              </div>
              <v-spacer></v-spacer>
              <v-btn dark color="#10AFA7">PUBLISH</v-btn>
            </div>
          </v-list-item-content>
        </v-list-item>
        <v-card-actions>
          <v-form @submit.prevent="createNews">
            <v-text-field
              v-model="news.title"
              class="text-h4 font-weight-bold"
              placeholder="Add title"
              required
            ></v-text-field>
            <v-file-input
              v-model="news.main_image"
              :rules="rules"
              accept="image/png, image/jpeg, image/bmp"
              placeholder="Pick an image"
              prepend-icon="mdi-camera"
            ></v-file-input>
            <v-textarea
              v-model="news.text"
              required
              placeholder="Type something"
            ></v-textarea>
            <v-btn type="submit"> Share News </v-btn>
          </v-form>
        </v-card-actions>
      </v-card-title>
    </v-card>
  </div>
</template>

<script>
export default {
  middleware: ['auth'],
  data: () => ({
    rules: [
      (value) =>
        !value ||
        value.size < 2000000 ||
        'Avatar size should be less than 2 MB!',
    ],
    news: {
      title: '',
      text: '',
      main_image: '',
    },
  }),
  methods: {
    async createNews() {
      const config = {
        headers: { 'content-type': 'multipart/form-data' },
      }
      const formData = new FormData()
      for (const data in this.news) {
        formData.append(data, this.news[data])
      }
      formData.append('author', this.$auth.user.id)
      try {
        await this.$axios.$post('news/news/', formData, config)
        this.$router.push('/')
      } catch (e) {
        // eslint-disable-next-line no-console
        console.log(e)
      }
    },
  },
}
</script>

<style scoped>
.v-card__actions {
  width: 100%;
}

form {
  width: 100%;
}
</style>
