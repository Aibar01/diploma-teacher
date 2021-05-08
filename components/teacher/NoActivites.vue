<template>
  <div class="d-flex flex-column justify-center align-center">
    <v-sheet
      id="circle"
      :rounded="rounded"
      height="200"
      width="200"
      color="#F1F1F1"
    ></v-sheet>
    <p>Your classmates have no activities yet :(</p>
    <p class="font-weight-bold">Go to Feed</p>
  </div>
</template>

<style scoped>
#info {
  height: 100%;
}
#circle {
  border-radius: 50%;
}
</style>
