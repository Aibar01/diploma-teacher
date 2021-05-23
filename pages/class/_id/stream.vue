<template>
  <div class="mt-10 pl-5">
    <v-card elevation="0" max-width="900">
      <v-card-title class="pb-0">
        <v-list-item class="pl-0 grow">
          <v-list-item-avatar color="#10AFA7">
            <img
              v-if="$auth.user.avatar"
              alt="Avatar"
              :src="$auth.user.avatar"
            />
            <img
              v-else
              alt="Avatar"
              src="https://avatars0.githubusercontent.com/u/9064066?v=4&s=460"
            />
          </v-list-item-avatar>

          <v-list-item-content>
            <v-form @submit.prevent="createAnnouncement">
              <div class="d-flex align-center">
                <div>
                  <v-text-field
                    v-model="announcement"
                    required
                    label="Хабарлама айтыңыз"
                  ></v-text-field>
                </div>
                <v-btn
                  :color="announcement.length > 10 ? `#10AFA7` : `#C6C4C4`"
                  dark
                  class="text-capitalize ml-5"
                  type="submit"
                  elevation="0"
                  >Жіберу</v-btn
                >
              </div>
            </v-form>
          </v-list-item-content>
        </v-list-item>
      </v-card-title>
    </v-card>
    <v-card v-if="announcements == []" max-width="500" outlined>
      <v-card-text>
        <p class="headline text--primary">Оқұшылармен жұмыс жасаңыз</p>
        <p>
          <v-icon class="pr-2" color="black" x-small>mdi-circle</v-icon
          >Материалдар қосыңыз
        </p>
        <p>
          <v-icon class="pr-2" color="black" x-small>mdi-circle</v-icon
          >Студенттерге жауап беріңіз
        </p>
      </v-card-text>
    </v-card>

    <v-card
      v-for="item in announcements.results"
      :key="item.id"
      outlined
      max-width="500"
      class="mt-8"
    >
      <v-card-title>
        <v-list-item class="pl-0 grow">
          <v-list-item-avatar>
            <img
              v-if="$auth.user.avatar"
              alt="Avatar"
              :src="$auth.user.avatar"
            />
            <img
              v-else
              alt="Avatar"
              src="https://avatars0.githubusercontent.com/u/9064066?v=4&s=460"
            />
          </v-list-item-avatar>

          <v-list-item-content>
            <div class="d-flex">
              <div>
                <v-list-item-title
                  >{{ $auth.user.first_name }}
                  {{ $auth.user.last_name }}</v-list-item-title
                >
                <v-list-item-subtitle
                  >12 Mar 2021 at 12:01</v-list-item-subtitle
                >
              </div>
              <v-spacer></v-spacer>
              <v-menu close-on-content-click="true" offset-y>
                <template #activator="{ on, attrs }">
                  <v-btn color="#C4C4C4" dark icon v-bind="attrs" v-on="on">
                    <v-icon dark> mdi-dots-horizontal </v-icon>
                  </v-btn>
                </template>
                <v-list>
                  <v-list-item>
                    <v-dialog v-model="editDialog" persistent max-width="600px">
                      <template #activator="{ on, attrs }">
                        <v-list-item-title
                          v-bind="attrs"
                          v-on="on"
                          @click="editText = item.annoucment_text"
                        >
                          Өзгерту
                        </v-list-item-title>
                      </template>
                      <v-card>
                        <v-card-title>
                          <span class="headline">Өзгерту</span>
                        </v-card-title>
                        <v-card-text>
                          <v-container>
                            <v-row>
                              <v-col cols="12">
                                <v-text-field
                                  v-model="editText"
                                  label="Өзгерту"
                                  required
                                ></v-text-field>
                              </v-col>
                            </v-row>
                          </v-container>
                        </v-card-text>
                        <v-card-actions>
                          <v-spacer></v-spacer>
                          <v-btn
                            text
                            class="text-capitalize"
                            @click="editDialog = false"
                          >
                            Болдырмау
                          </v-btn>
                          <v-btn
                            color="#10AFA7"
                            text
                            class="text-capitalize"
                            @click="editAnnouncment(item.id)"
                          >
                            Өзгерту
                          </v-btn>
                        </v-card-actions>
                      </v-card>
                    </v-dialog>
                  </v-list-item>
                  <v-list-item>
                    <v-dialog v-model="dialog" persistent max-width="300">
                      <template #activator="{ on, attrs }">
                        <v-list-item-title v-bind="attrs" v-on="on"
                          >Жою</v-list-item-title
                        >
                      </template>
                      <v-card>
                        <v-card-title class="headline">
                          Хабарламаны жою?
                        </v-card-title>
                        <v-card-text>Бұл кайтарылмайтын әрекет.</v-card-text>
                        <v-card-actions>
                          <v-spacer></v-spacer>
                          <v-btn
                            text
                            class="text-capitalize"
                            @click="dialog = false"
                          >
                            Болдырмау
                          </v-btn>
                          <v-btn
                            color="#10AFA7"
                            text
                            class="text-capitalize"
                            @click="deleteAnnouncment(item.id)"
                          >
                            Жою
                          </v-btn>
                        </v-card-actions>
                      </v-card>
                    </v-dialog>
                  </v-list-item>
                </v-list>
              </v-menu>
            </div>
          </v-list-item-content>
        </v-list-item>
      </v-card-title>

      <v-card-text class="font-weight-bold">
        {{ item.annoucment_text }}
      </v-card-text>
    </v-card>
  </div>
</template>

<script>
export default {
  layout: 'class',
  middleware: 'auth',
  async asyncData({ $axios, params }) {
    try {
      const announcements = await $axios.$get(`classes/announcment/`, {
        params: { class: params.id },
      })
      return {
        announcements,
      }
    } catch (e) {
      return {
        announcements: [],
      }
    }
  },
  data() {
    return {
      dialog: false,
      editDialog: false,
      announcement: '',
      editText: '',
      announcements: [],
      items: [
        { title: 'Move to top' },
        { title: 'Copy link' },
        { title: 'Edit' },
        { title: 'Delete' },
      ],
    }
  },
  methods: {
    async createAnnouncement() {
      try {
        await this.$axios.$post('classes/announcment/', {
          annoucment_text: this.announcement,
          scratch_class: this.$route.params.id,
        })
        this.announcement = ''
        this.announcements = await this.$axios.$get(`classes/announcment/`, {
          params: { class: this.$route.params.id },
        })
      } catch (e) {
        // eslint-disable-next-line no-console
        console.log(e)
      }
    },
    async deleteAnnouncment(id) {
      try {
        await this.$axios.$delete(`classes/announcment/${id}`)
        this.dialog = false
      } catch (err) {
        // eslint-disable-next-line no-console
        console.log(err)
      }

      this.announcements = await this.$axios.$get(`classes/announcment/`, {
        params: { class: this.$route.params.id },
      })
    },
    async editAnnouncment(id) {
      try {
        await this.$axios.$patch(`classes/announcment/${id}/`, {
          annoucment_text: this.editText,
          scratch_class: this.$route.params.id,
        })
        this.announcement = ''
      } catch (err) {
        // eslint-disable-next-line no-console
        console.log(err)
      }

      this.announcements = await this.$axios.$get(`classes/announcment/`, {
        params: { class: this.$route.params.id },
      })

      this.editDialog = false
    },
  },
}
</script>
