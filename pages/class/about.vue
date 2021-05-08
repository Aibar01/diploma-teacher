<template>
  <v-card class="pl-5 pt-5" elevation="0" max-width="700">
    <v-row>
      <v-col class="font-weight-bold text-uppercase">About course</v-col>
      <v-col>
        <v-textarea
          outlined
          name="input-7-4"
          label="Outlined textarea"
          value="The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through."
        ></v-textarea>
      </v-col>
    </v-row>
    <v-row>
      <v-col class="font-weight-bold text-uppercase">Teacher</v-col>
      <v-col>
        <v-card elevation="0" max-width="800">
          <v-card-title class="pt-0">
            <v-list-item class="pl-0 grow">
              <v-list-item-avatar color="#10AFA7">
                <img
                  alt="Avatar"
                  src="https://avatars0.githubusercontent.com/u/9064066?v=4&s=460"
                />
              </v-list-item-avatar>

              <v-list-item-content>
                <v-list-item-title> John Doe. </v-list-item-title>
              </v-list-item-content>
            </v-list-item>
          </v-card-title>
        </v-card>
      </v-col>
    </v-row>
    <v-card-actions>
      <v-btn class="text-capitalize" color="#10AFA7" dark> Save </v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  layout: 'class',
}
</script>
