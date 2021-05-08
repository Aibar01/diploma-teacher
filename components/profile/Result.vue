<template>
  <v-row>
    <v-col>
      <v-card outlined class="mx-auto" max-width="400">
        <v-list-item two-line>
          <v-list-item-content>
            <v-list-item-title class="headline"> Classes </v-list-item-title>
          </v-list-item-content>
        </v-list-item>

        <v-card-text>
          <v-row align="center">
            <v-col d-flex justify="center" align="center" cols="6">
              <v-row>
                <v-col class="display-3" cols="12">4</v-col>
                <v-col cols="12">Classes</v-col>
              </v-row>
            </v-col>
            <v-col cols="6">
              <v-row>
                <v-col cols="12">Public</v-col>
                <v-col cols="12" class="body-1 pt-0">
                  <strong>1 class</strong>
                </v-col>
              </v-row>
              <v-row>
                <v-col cols="12">Private</v-col>
                <v-col cols="12" class="body-1 pt-0">
                  <strong>3 classes</strong>
                </v-col>
              </v-row>
            </v-col>
          </v-row>
        </v-card-text>
      </v-card>
    </v-col>
    <v-col>
      <v-card outlined class="mx-auto" max-width="400">
        <v-list-item two-line>
          <v-list-item-content>
            <v-list-item-title class="headline"> Grades </v-list-item-title>
          </v-list-item-content>
        </v-list-item>

        <v-card-text>
          <v-row align="center">
            <v-col d-flex justify="center" align="center" cols="6">
              <v-row>
                <v-col class="display-3" cols="12"> 93% </v-col>
                <v-col cols="12">Grades</v-col>
              </v-row>
            </v-col>
            <v-col cols="6">
              <v-row>
                <v-col cols="12">Quizes</v-col>
                <v-col cols="12" class="body-1 pt-0">
                  <strong>95% overall</strong>
                </v-col>
              </v-row>
              <v-row>
                <v-col cols="12">Assignments</v-col>
                <v-col cols="12" class="body-1 pt-0">
                  <strong>98% overall</strong>
                </v-col>
              </v-row>
            </v-col>
          </v-row>
        </v-card-text>
      </v-card>
    </v-col>
  </v-row>
</template>
