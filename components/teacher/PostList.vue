<template>
  <div>
    <div id="parent">
      <div class="mr-md-6"><AvatarCard /></div>
      <div><PostCard /></div>
    </div>
  </div>
</template>

<script>
import AvatarCard from './AvatarCard'
import PostCard from './PostCard'

export default {
  components: {
    PostCard,
    AvatarCard,
  },
}
</script>

<style scoped>
#parent {
  display: grid;
  grid-template-columns: 1fr 4fr;
}
</style>
