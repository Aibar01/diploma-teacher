<template>
  <v-container fluid>
    <v-row class="pt-5 pl-5">
      <v-col cols="12" class="py-0">
        <p class="font-weight-bold">App Name – We make learning easy!</p>
      </v-col>
      <v-col cols="12" class="py-0">
        <p class="text-uppercase" style="color: #999999">Contacts</p>
      </v-col>
      <v-col cols="12" class="py-0">
        <p class="font-weight-bold mb-0">+7 708 654 3454</p>
      </v-col>
      <v-col cols="12" class="py-0">
        <p class="font-weight-bold">Almaty, Kazakhstan</p>
      </v-col>
      <v-col cols="12" class="py-0">
        <p style="color: #10afa7">support@gmail.com</p>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  layout(context) {
    return 'about'
  },
}
</script>
