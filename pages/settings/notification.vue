<template>
  <v-container class="px-0 mt-5 ml-5" fluid>
    <v-row>
      <v-col style="display: flex" class="pb-0">
        <v-checkbox id="notification" class="pd-0 mt-0" />
        <label for="notification">Send Push-notifications</label>
      </v-col>
    </v-row>
    <v-row class="mt-0">
      <v-col class="pt-0 ml-9">
        <p class="caption">
          Allow us to send you notifications in order to help you to submit all
          homeworks.
        </p>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  layout(context) {
    return 'profile'
  },
}
</script>

<style scoped>
.v-input--selection-controls {
  margin-top: 0;
  padding-top: 0;
}

p {
  color: #999999;
}
</style>
