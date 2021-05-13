<template>
  <v-card elevation="0" class="mt-10" max-width="1000">
    <v-img
      class="white--text align-end"
      max-height="420px"
      max-width="100%"
      :src="item.main_image"
    >
    </v-img>

    <v-card-subtitle class="pb-0">
      <v-icon small class="pb-1"> mdi-calendar-blank-outline </v-icon>
      {{ $moment(new Date(+item.created_date * 1000)).format('MMM D, YYYY') }}
    </v-card-subtitle>

    <v-card-title>
      <strong> {{ item.title }} </strong>
    </v-card-title>

    <v-card-text class="text--primary">
      <div>{{ item.text.split(' ').slice(0, 100).join(' ') }}...</div>
    </v-card-text>

    <v-card-actions>
      <v-btn color="black" class="text-capitalize" text>
        <NuxtLink :to="`/news/${item.id}`">
          <strong> Read more </strong>
        </NuxtLink>
      </v-btn>
      <v-spacer></v-spacer>
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
}
</script>

<style scoped>
a {
  text-decoration: none;
  color: #10afa7;
}
</style>
