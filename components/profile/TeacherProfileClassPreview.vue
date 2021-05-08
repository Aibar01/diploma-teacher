<template>
  <v-item-group active-class="primary">
    <v-container>
      <v-row>
        <v-col v-for="n in 3" :key="n" cols="12" md="4">
          <v-item>
            <v-card outlined class="mx-auto" max-width="344">
              <v-img
                src="https://www.schooleducationgateway.eu/files/png5/ebeginswlanguage.png"
                height="200px"
              ></v-img>

              <v-card-title> Introduction to Scratch </v-card-title>

              <v-card-subtitle> Recommended </v-card-subtitle>
            </v-card>
          </v-item>
        </v-col>
      </v-row>
    </v-container>
  </v-item-group>
</template>
