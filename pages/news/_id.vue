<template>
  <div>
    <v-container class="mt-5">
      <v-row>
        <v-col>
          <div>
            <NuxtLink to="/" prefetch class="d-flex align-center">
              <v-icon>mdi-arrow-left</v-icon>
              <div class="text-capitalize font-weight-bold">Back to Main</div>
            </NuxtLink>
          </div>
        </v-col>
      </v-row>
    </v-container>
    <div class="d-flex justify-center">
      <PostDetail :item="item" />
    </div>
  </div>
</template>

<script>
import PostDetail from '../../components/post/PostDetail'
export default {
  components: {
    PostDetail,
  },
  async asyncData({ $axios, params }) {
    try {
      const item = await $axios.$get(`news/news/${params.id}`)
      return {
        item,
      }
    } catch (e) {
      return {
        item: {},
      }
    }
  },
  data() {
    return {
      item: {},
    }
  },
}
</script>
