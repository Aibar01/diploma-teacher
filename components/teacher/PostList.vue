<template>
  <div>
    <div v-if="item" id="parent">
      <v-card elevation="0" class="ml-lg-12 ml-sm-0 mt-10" max-width="170">
        <!-- <img
          
          class="white--text align-end"
          height="170"
          :src="`${item.author.avatar}?size=170`"
        /> -->

        <picture v-if="item.author.avatar">
          <source :src="item.author.avatar" type="image/webp" />
          <img
            :src="item.author.avatar"
            :srcSet="item.author.avatar"
            width="170"
            height="170"
            sizes="(min-width: 1024px) 1024px, 100vw"
            loading="lazy"
          />
        </picture>

        <img v-else src="~/assets/img/abylai.png" height="170" loading="lazy" />
        <v-card-title v-if="item.author" class="pb-0 subtitle-2">
          {{ item.author.first_name }} {{ item.author.last_name }}
        </v-card-title>
        <v-card-subtitle
          v-if="item.author.user_type === 'teacher'"
          class="pt-4 caption"
        >
          Мұғалім
        </v-card-subtitle>
        <v-card-subtitle v-else class="pt-4 caption"> Оқушы </v-card-subtitle>
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
