<template>
  <div>
    <NoActivites v-if="noActivites" />
    <div v-else>
      <div class="d-flex align-center ml-16 mt-10">
        <div class="headline">Discovered something new?</div>
        <v-btn
          to="news/create"
          dark
          color="#10AFA7"
          class="text-capitalize ml-12"
          >Share news</v-btn
        >
      </div>
      <div class="ml-12 mt-10">
        <div class="text-uppercase">Other Teachers Sharing</div>
      </div>
      <PostList v-for="item in items" :key="item" />
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
  data() {
    return {
      noActivites: false,
      items: [1, 2, 3, 4],
    }
  },
}
</script>

<style scoped>
a {
  color: white !important;
}
</style>
