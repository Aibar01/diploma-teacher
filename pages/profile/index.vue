<template>
  <Profile />
</template>

<script>
import Profile from '../../components/profile/Profile'

export default {
  components: {
    Profile,
  },
  layout(context) {
    return 'detail'
  },
}
</script>
