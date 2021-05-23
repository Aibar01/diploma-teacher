<template>
  <div>
    <NoActivites v-if="noActivites" />
    <div v-else>
      <div v-if="$auth.loggedIn" class="d-flex align-center ml-16 mt-10">
        <div class="headline">Жаңа бірдеңе біліп алдыңыз ба?</div>
        <v-btn
          to="news/create"
          dark
          color="#10AFA7"
          class="text-capitalize ml-12"
          elevation="0"
          >Бөлісу</v-btn
        >
      </div>
      <div class="ml-12 mt-10">
        <div class="text-uppercase">Адамдардың бөліскені</div>
      </div>
      <div v-for="item in items.results" :key="item.id">
        <PostList :item="item" />
      </div>
    </div>
  </div>
</template>

<script>
import NoActivites from '../components/teacher/NoActivites'
import PostList from '../components/teacher/PostList'

export default {
  components: {
    NoActivites,
    PostList,
  },
  async asyncData({ $axios }) {
    try {
      const items = await $axios.$get(`/news/news/`)
      return { items }
    } catch (e) {
      return { items: [] }
    }
  },
  data() {
    return {
      noActivites: false,
    }
  },
}
</script>

<style scoped>
a {
  color: white !important;
}
</style>
