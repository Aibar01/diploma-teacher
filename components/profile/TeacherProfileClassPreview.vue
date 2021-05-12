<template>
  <v-item-group active-class="primary">
    <v-container>
      <v-row>
        <v-col
          v-for="item in $auth.user.classes.slice(0, 3)"
          :key="item.id"
          cols="12"
          md="4"
        >
          <v-item>
            <v-card outlined class="mx-auto" max-width="344">
              <v-img
                v-if="item.class_image"
                :src="item.class_image"
                height="200px"
              ></v-img>
              <v-img
                v-else
                src="https://www.schooleducationgateway.eu/files/png5/ebeginswlanguage.png"
                height="200px"
              ></v-img>
              <v-card-title> {{ item.class_name }} </v-card-title>

              <v-card-subtitle> Recommended </v-card-subtitle>
            </v-card>
          </v-item>
        </v-col>
      </v-row>
    </v-container>
  </v-item-group>
</template>
