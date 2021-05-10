<template>
  <v-app dark>
    <v-navigation-drawer
      v-model="drawer"
      :mini-variant="miniVariant"
      :clipped="clipped"
      fixed
      app
    >
      <v-list-item class="py-2">
        <v-list-item-content>
          <v-list-item-title>Aibar Bekkozhayev</v-list-item-title>
        </v-list-item-content>
      </v-list-item>

      <v-divider></v-divider>

      <v-list dense nav>
        <v-list-item v-for="item in items" :key="item.title" link>
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <NuxtLink :to="item.to">
              <v-list-item-title>{{ item.title }}</v-list-item-title>
            </NuxtLink>
          </v-list-item-content>
        </v-list-item>
        <v-list-item link>
          <v-list-item-icon>
            <v-icon>mdi-plus-circle-outline</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>
              <v-dialog v-model="dialog" persistent max-width="600px">
                <template #activator="{ on, attrs }">
                  <div v-bind="attrs" v-on="on">Create Class</div>
                </template>
                <v-card>
                  <v-card-title class="d-flex justify-center">
                    <span class="headline">Create a class</span>
                  </v-card-title>
                  <v-divider class="pt-5"></v-divider>
                  <v-card-text>
                    <v-container>
                      <v-row>
                        <v-col cols="12">
                          <v-text-field
                            label="Class name"
                            placeholder="Enter class name"
                            outlined
                          ></v-text-field>
                        </v-col>
                        <v-col cols="12">
                          <v-text-field
                            label="Subject"
                            placeholder="Enter subject name"
                            outlined
                          ></v-text-field>
                        </v-col>
                        <v-col cols="12" class="pt-0">
                          <v-radio-group label="Type of class" class="mt-0">
                            <div class="d-flex align-start">
                              <v-radio
                                class="pr-5"
                                label="Public"
                                value="Public"
                              ></v-radio>
                              <v-radio
                                label="Private"
                                value="Private"
                              ></v-radio>
                            </div>
                          </v-radio-group>
                        </v-col>
                      </v-row>
                    </v-container>
                  </v-card-text>
                  <v-card-actions class="d-flex justify-center pb-5">
                    <v-btn
                      color="#10AFA7"
                      dark
                      class="text-capitalize"
                      @click="dialog = false"
                    >
                      Save
                    </v-btn>
                  </v-card-actions>
                </v-card>
              </v-dialog>
            </v-list-item-title>
          </v-list-item-content>
        </v-list-item>
        <v-list-item link>
          <v-list-item-icon>
            <v-icon>mdi-circle</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <NuxtLink to="/class/stream">
              <v-list-item-title>Scratch NEW CLASS</v-list-item-title>
            </NuxtLink>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar :clipped-left="clipped" fixed app>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-tabs>
        <v-tabs-slider color="#353232"></v-tabs-slider>
        <v-tab class="text-capitalize">Feed</v-tab>
        <!-- <v-tab class="text-capitalize">Students Activity</v-tab> -->
      </v-tabs>
      <v-spacer />
      <v-text-field
        class="pt-4 pr-6"
        label="Search classes, teachers"
        prepend-icon="mdi-magnify"
      ></v-text-field>
    </v-app-bar>
    <v-main>
      <nuxt />
    </v-main>
    <v-footer :absolute="!fixed" app>
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      dialog: false,
      clipped: false,
      drawer: true,
      fixed: true,
      items: [
        {
          title: 'Feed',
          icon: 'mdi-view-dashboard',
          to: '/',
        },
        {
          title: 'Notifications',
          icon: 'mdi-bell',
          to: '/notification',
        },
      ],
      miniVariant: false,
      right: true,
      title: 'Diploma',
    }
  },
}
</script>

<style>
* {
  font-family: 'Rubik', sans-serif;
}

.v-input--selection-controls .v-input__control {
  width: 100%;
}
.v-tab {
  color: #10afa7;
}
.v-application .primary--text {
  color: #10afa7 !important;
  caret-color: #10afa7 !important;
}

/* .v-text-field > .v-input__control > .v-input__slot:before {
  border-color: transparent !important;
}
.v-text-field > .v-input__control > .v-input__slot:hover {
  border-color: transparent !important;
} */
</style>
