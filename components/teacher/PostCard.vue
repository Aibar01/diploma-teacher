<template>
  <v-card elevation="0" class="mt-10" max-width="1000">
    <v-img
      class="white--text align-end"
      max-height="420px"
      max-width="100%"
      src="https://keystoneacademic-res.cloudinary.com/image/upload/f_auto,q_auto,c_fill,w_1920/element/13/132557_UnicafHL.jpg"
    >
    </v-img>

    <v-card-subtitle class="pb-0">
      <v-icon small class="pb-1"> mdi-calendar-blank-outline </v-icon>
      Sep 8, 2020
    </v-card-subtitle>

    <v-card-title>
      <strong> Here will be One lined Post title 2021 </strong>
    </v-card-title>

    <v-card-text class="text--primary">
      <div>
        We are about to start the new year 2021 and the last year has been quite
        different and influenced the way we designed a lot. But let’s not talk
        about the last year but rather focus on the future! I am working as an
        in...
      </div>
    </v-card-text>

    <v-card-actions>
      <v-btn color="black" class="text-capitalize" text>
        <NuxtLink :to="`/activites/${1}`">
          <strong> Read more </strong>
        </NuxtLink>
      </v-btn>
      <v-spacer></v-spacer>
      <v-icon>mdi-heart-outline</v-icon>
    </v-card-actions>
  </v-card>
</template>

<style scoped>
a {
  text-decoration: none;
  color: #10afa7;
}
</style>
