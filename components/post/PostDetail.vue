<template>
  <v-card elevation="0" class="my-10" max-width="1000">
    <v-card-title>
      <strong> {{ item.title }} </strong>
    </v-card-title>

    <v-card-subtitle class="pt-4 pb-6">
      <v-icon small class="pb-1"> mdi-calendar-blank-outline </v-icon>
      {{ $moment(new Date(+item.created_date * 1000)).format('MMM D, YYYY') }}
    </v-card-subtitle>
    <v-img
      class="white--text align-end"
      max-height="420px"
      max-width="100%"
      :src="item.main_image"
    >
    </v-img>

    <v-card-text class="text--primary">
      <div>
        {{ item.text }}
      </div>
    </v-card-text>
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
