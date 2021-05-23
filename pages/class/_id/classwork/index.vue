<template>
  <div class="mt-10 pl-5">
    <v-card class="pb-5" elevation="0" max-width="900">
      <v-card-title class="pb-0">
        <v-menu
          :close-on-content-click="closeOn"
          transition="slide-y-transition"
          offset-y
          bottom
        >
          <template #activator="{ on, attrs }">
            <v-btn
              elevation="0"
              class="py-4"
              color="#10AFA7"
              dark
              v-bind="attrs"
              v-on="on"
            >
              <v-icon class="pr-2">mdi-plus-circle-outline</v-icon> Құрастыру
            </v-btn>
          </template>
          <v-list>
            <template v-for="(item, i) in items">
              <CardDialog :key="i" :item="item" @getItems="getItems" />
            </template>
          </v-list>
        </v-menu>
      </v-card-title>
    </v-card>

    <v-card max-width="500" outlined>
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
      v-for="i in classworks.results"
      :key="i.id"
      outlined
      max-width="500"
      class="mt-8"
    >
      <v-card-title>
        <v-list-item class="pl-0 grow">
          <nuxt-link :to="`classwork/${i.id}`">
            <v-list-item-avatar color="#10AFA7">
              <span class="white--text headline">
                <v-icon dark>mdi-notebook</v-icon>
              </span>
            </v-list-item-avatar>
          </nuxt-link>
          <v-list-item-content>
            <div class="d-flex">
              <nuxt-link :to="`classwork/${i.id}`">
                <div>
                  <v-list-item-title>{{ i.title }}</v-list-item-title>
                  <v-list-item-subtitle>{{
                    $moment(new Date(+i.created_at * 1000)).format(
                      'D MMM YYYY, h:mm'
                    )
                  }}</v-list-item-subtitle>
                </div>
              </nuxt-link>
              <v-spacer></v-spacer>
              <v-menu offset-y>
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
                          @click="editClasswork = { ...i }"
                        >
                          Өзгерту
                        </v-list-item-title>
                      </template>
                      <v-card>
                        <v-form @submit.prevent="updateClasswork(i.id)">
                          <v-card-title class="pl-10">
                            <span class="headline font-weight-bold"
                              >Өзгерту {{ editClasswork.title }}</span
                            >
                          </v-card-title>
                          <v-card-text>
                            <v-container>
                              <v-row>
                                <v-col cols="12">
                                  <v-text-field
                                    v-model="editClasswork.title"
                                    outlined
                                    label="Тақырып"
                                    placeholder="Тақырып"
                                    required
                                  ></v-text-field>
                                </v-col>
                                <v-col cols="12">
                                  <v-textarea
                                    v-model="editClasswork.description"
                                    outlined
                                    name="input-7-4"
                                    label="Сипаттама"
                                    placeholder="(қосымша)"
                                  ></v-textarea>
                                </v-col>
                                <v-col cols="12" class="d-flex">
                                  <v-file-input
                                    v-model="editClasswork.uploaded_file"
                                    color="#10AFA7"
                                    label="Қосу"
                                    outlined
                                  ></v-file-input>
                                </v-col>
                                <v-col v-if="editClasswork.due_date" cols="12">
                                  <v-menu
                                    ref="menu"
                                    v-model="menu"
                                    :close-on-content-click="false"
                                    :return-value.sync="date"
                                    transition="scale-transition"
                                    offset-y
                                    min-width="auto"
                                  >
                                    <template #activator="{ on, attrs }">
                                      <v-text-field
                                        v-model="date"
                                        label="Дейін уақыт"
                                        prepend-icon="mdi-calendar"
                                        readonly
                                        v-bind="attrs"
                                        v-on="on"
                                      ></v-text-field>
                                    </template>
                                    <v-date-picker
                                      v-model="date"
                                      no-title
                                      scrollable
                                    >
                                      <v-spacer></v-spacer>
                                      <v-btn
                                        text
                                        color="#10AFA7"
                                        @click="editMenu = false"
                                      >
                                        Болдырмау
                                      </v-btn>
                                      <v-btn
                                        text
                                        color="#10AFA7"
                                        @click="$refs.menu.save(date)"
                                      >
                                        Құрастыру
                                      </v-btn>
                                    </v-date-picker>
                                  </v-menu>
                                </v-col>
                                <v-col v-if="editClasswork.due_date" cols="12">
                                  <v-menu
                                    ref="time"
                                    v-model="menu2"
                                    :close-on-content-click="false"
                                    transition="scale-transition"
                                    offset-y
                                    min-width="auto"
                                  >
                                    <template #activator="{ on, attrs }">
                                      <v-text-field
                                        v-model="time"
                                        label="Due time"
                                        prepend-icon="mdi-watch"
                                        readonly
                                        v-bind="attrs"
                                        v-on="on"
                                      ></v-text-field>
                                    </template>
                                    <v-time-picker
                                      v-model="time"
                                      ampm-in-title
                                      format="ampm"
                                    >
                                      <v-spacer></v-spacer>
                                      <v-btn
                                        text
                                        color="#10AFA7"
                                        @click="menu2 = false"
                                      >
                                        Құрастыру
                                      </v-btn>
                                    </v-time-picker>
                                  </v-menu>
                                </v-col>
                              </v-row>
                            </v-container>
                          </v-card-text>
                          <v-card-actions class="pb-10 pl-10">
                            <v-btn
                              elevation="0"
                              class="text-capitalize"
                              color="#10AFA7"
                              dark
                              type="submit"
                            >
                              Өзгерту
                            </v-btn>
                            <v-btn
                              elevation="0"
                              class="text-capitalize"
                              text
                              @click="editDialog = false"
                            >
                              Болдырмау
                            </v-btn>
                          </v-card-actions>
                        </v-form>
                      </v-card>
                    </v-dialog>
                  </v-list-item>
                  <v-list-item>
                    <v-dialog v-model="dialog" persistent max-width="300">
                      <template #activator="{ on, attrs }">
                        <v-list-item-title v-bind="attrs" v-on="on"
                          >Delete</v-list-item-title
                        >
                      </template>
                      <v-card>
                        <v-card-title class="headline">
                          Delete classwork?
                        </v-card-title>
                        <v-card-text>This action is unrecoveravle.</v-card-text>
                        <v-card-actions>
                          <v-spacer></v-spacer>
                          <v-btn
                            text
                            class="text-capitalize"
                            @click="dialog = false"
                          >
                            Cancel
                          </v-btn>
                          <v-btn
                            color="#10AFA7"
                            text
                            class="text-capitalize"
                            @click="deleteClasswork(i.id)"
                          >
                            Delete
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
      <v-card-text v-if="i.description" class="font-weight-bold">
        {{ i.description }}
      </v-card-text>
      <v-card-text v-if="i.due_date" class="font-weight-bold">
        Due to
        {{ $moment(new Date(+i.due_date * 1000)).format('D MMM YYYY, h:mm') }}
      </v-card-text>
    </v-card>
  </div>
</template>

<script>
import CardDialog from '../../../../components/classwork/CardDialog'

export default {
  components: {
    CardDialog,
  },
  layout: 'class',
  middleware: 'auth',
  async asyncData({ $axios, params }) {
    try {
      const classworks = await $axios.$get(`classes/classworkes/`, {
        params: { class: params.id },
      })
      return {
        classworks,
      }
    } catch (err) {
      return { classworks: [] }
    }
  },
  data() {
    return {
      editClasswork: {
        title: '',
        description: '',
        uploaded_file: null,
      },
      dialog: false,
      editDialog: false,
      editMenu: false,
      closeOn: true,
      classworks: [],
      date: '',
      time: '',
      menu: false,
      menu2: false,
      items: [
        { title: 'Сабақ', icon: 'mdi-circle' },
        { title: 'Ұй жұмысы', icon: 'mdi-circle' },
        { title: 'Материал', icon: 'mdi-circle' },
      ],
    }
  },
  methods: {
    async getItems() {
      try {
        this.classworks = await this.$axios.$get(`classes/classworkes/`, {
          params: { class: this.$route.params.id },
        })
      } catch (err) {
        // eslint-disable-next-line no-console
        console.log(err)
      }
    },
    async deleteClasswork(id) {
      try {
        await this.$axios.$delete(`classes/classworkes/${id}/`)

        this.classworks = await this.$axios.$get(`classes/classworkes/`, {
          params: { class: this.$route.params.id },
        })
      } catch (err) {
        // eslint-disable-next-line no-console
        console.log(err)
      }
    },
    async updateClasswork(id) {
      if (this.date && this.time) {
        this.editClasswork.due_date =
          this.date.toString() + ' ' + this.time.toString()
      }

      const config = {
        headers: { 'content-type': 'multipart/form-data' },
      }

      const formData = new FormData()
      for (const data in this.editClasswork) {
        formData.append(data, this.editClasswork[data])
      }

      try {
        await this.$axios.$patch(`classes/classworkes/${id}/`, formData, config)
        this.classworks = await this.$axios.$get(`classes/classworkes/`)
        this.editDialog = false
        this.editClasswork = {
          title: '',
          description: '',
          uploaded_file: '',
        }
      } catch (err) {
        // eslint-disable-next-line no-console
        console.log(err)
      }
    },
  },
}
</script>
