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
            <img
              alt="Avatar"
              src="https://avatars0.githubusercontent.com/u/9064066?v=4&s=460"
            />
          </v-list-item-avatar>

          <v-list-item-content>
            <div class="d-flex">
              <div>
                <v-list-item-title> Aidyn Jomart </v-list-item-title>
                <v-list-item-subtitle> Writing new </v-list-item-subtitle>
              </div>
              <v-spacer></v-spacer>
              <v-btn dark color="#10AFA7">PUBLISH</v-btn>
            </div>
          </v-list-item-content>
        </v-list-item>
        <v-card-actions>
          <v-form>
            <v-text-field
              class="text-h4 font-weight-bold"
              placeholder="Add title"
            ></v-text-field>
            <v-file-input
              :rules="rules"
              accept="image/png, image/jpeg, image/bmp"
              placeholder="Pick an image"
              prepend-icon="mdi-camera"
            ></v-file-input>
            <v-textarea placeholder="Type something"></v-textarea>
          </v-form>
        </v-card-actions>
      </v-card-title>
    </v-card>
  </div>
</template>

<script>
export default {
  data: () => ({
    rules: [
      (value) =>
        !value ||
        value.size < 2000000 ||
        'Avatar size should be less than 2 MB!',
    ],
  }),
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
