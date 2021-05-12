<template>
  <div>
    <div v-if="item" id="parent">
      <v-card elevation="0" class="ml-lg-12 ml-sm-0 mt-10" max-width="170">
        <v-img
          v-if="item.author.avatar"
          class="white--text align-end"
          height="170px"
          :src="item.author.avatar"
        >
        </v-img>
        <v-img
          v-else
          class="white--text align-end"
          height="170px"
          src="/uploads/avatars/72/5cbddabff083e-bpfull.jpg"
        >
        </v-img>
        <v-card-title v-if="item.author" class="pb-0 subtitle-2">
          {{ item.author.first_name }} {{ item.author.last_name }}
        </v-card-title>
        <v-card-subtitle class="pt-4 caption">
          Programming оқушы
        </v-card-subtitle>
      </v-card>
      <div><PostCard :item="item" /></div>
    </div>
  </div>
</template>

<script>
import PostCard from './PostCard'

export default {
  components: {
    PostCard,
  },
  props: {
    // eslint-disable-next-line vue/require-default-prop
    item: Object,
  },
}
</script>

<style scoped>
#parent {
  display: grid;
  grid-template-columns: 1fr 4fr;
}
</style>
