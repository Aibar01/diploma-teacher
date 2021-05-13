<template>
  <v-list-item>
    <v-dialog v-model="dialog" max-width="600px">
      <template #activator="{ on, attrs }">
        <v-list-item-title v-bind="attrs" v-on="on">
          <v-icon color="#10AFA7">{{ item.icon }}</v-icon>
          {{ item.title }}
        </v-list-item-title>
      </template>
      <v-card>
        <v-form @submit.prevent="createItem(item.title)">
          <v-card-title class="pl-10">
            <span class="headline font-weight-bold"
              >Create {{ item.title }}</span
            >
          </v-card-title>
          <v-card-text>
            <v-container>
              <v-row>
                <v-col cols="12">
                  <v-text-field
                    v-model="newItem.title"
                    outlined
                    label="Title"
                    placeholder="Enter title"
                    required
                  ></v-text-field>
                </v-col>
                <v-col cols="12">
                  <v-textarea
                    v-model="newItem.description"
                    outlined
                    name="input-7-4"
                    label="Description"
                    placeholder="(optional)"
                  ></v-textarea>
                </v-col>
                <v-col cols="12" class="d-flex">
                  <v-file-input
                    v-model="newItem.uploaded_file"
                    color="#10AFA7"
                    label="Add"
                    outlined
                  ></v-file-input>
                </v-col>
                <v-col v-if="item.title == 'Homework'" cols="12">
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
                        label="Due date"
                        prepend-icon="mdi-calendar"
                        readonly
                        v-bind="attrs"
                        v-on="on"
                      ></v-text-field>
                    </template>
                    <v-date-picker v-model="date" no-title scrollable>
                      <v-spacer></v-spacer>
                      <v-btn text color="#10AFA7" @click="menu = false">
                        Cancel
                      </v-btn>
                      <v-btn
                        text
                        color="#10AFA7"
                        @click="$refs.menu.save(date)"
                      >
                        OK
                      </v-btn>
                    </v-date-picker>
                  </v-menu>
                </v-col>
                <v-col v-if="item.title == 'Homework'" cols="12">
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
                    <v-time-picker v-model="time" ampm-in-title format="ampm">
                      <v-spacer></v-spacer>
                      <v-btn text color="#10AFA7" @click="menu2 = false">
                        OK
                      </v-btn>
                    </v-time-picker>
                  </v-menu>
                </v-col>
              </v-row>
            </v-container>
          </v-card-text>
          <v-card-actions class="pb-10 pl-10">
            <v-btn class="text-capitalize" color="#10AFA7" dark type="submit">
              Create lesson
            </v-btn>
            <v-btn class="text-capitalize" text @click="dialog = false">
              Cancel
            </v-btn>
          </v-card-actions>
        </v-form>
      </v-card>
    </v-dialog>
  </v-list-item>
</template>

<script>
export default {
  // eslint-disable-next-line vue/require-prop-types
  props: ['item'],
  data() {
    return {
      dialog: false,
      date: new Date().toISOString().substr(0, 10),
      time: '12:00',
      menu: false,
      menu2: false,
      newItem: {
        title: '',
        description: '',
        uploaded_file: null,
        due_date: '',
      },
      classworks: [],
    }
  },
  methods: {
    async createItem(type) {
      this.newItem.due_date = this.date.toString() + ' ' + this.time.toString()

      type = type.toLowerCase()

      const config = {
        headers: { 'content-type': 'multipart/form-data' },
      }
      const formData = new FormData()
      for (const data in this.newItem) {
        formData.append(data, this.newItem[data])
      }

      formData.append('scratch_class', this.$route.params.id)
      formData.append('classwork_type', this.item.title.toLowerCase())

      try {
        await this.$axios.$post(`classes/classworkes/`, formData, config)
        this.classwork = await this.$axios.$get(`classes/classworkes/`)
        this.dialog = false
        this.newItem = {
          title: '',
          description: '',
          uploaded_file: '',
          due_date: '',
        }
        this.$emit('getItems')
      } catch (err) {
        // eslint-disable-next-line no-console
        console.log(err)
      }
    },
  },
}
</script>
