<template>
  <v-card outlined class="ml-lg-12 ml-sm-0 mt-10" max-width="170">
    <v-img
      class="white--text align-end"
      height="170px"
      src="https://aardvark.ghostpool.com/original/wp-content/uploads/avatars/72/5cbddabff083e-bpfull.jpg"
    >
    </v-img>
    <v-card-title class="pb-0 subtitle-2"> Али Osman </v-card-title>
    <v-card-subtitle
      v-if="$auth.user.user_type === 'teacher'"
      class="pt-4 caption"
    >
      Мұғалім
    </v-card-subtitle>
    <v-card-subtitle v-else class="pt-4 caption"> Оқушы </v-card-subtitle>
  </v-card>
</template>
