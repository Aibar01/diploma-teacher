<template>
  <v-container fluid>
    <v-row>
      <v-col cols="6">
        <v-simple-table v-if="items">
          <template #default>
            <thead class="background-color:#999999 !important">
              <tr>
                <th class="text-left text-capitalize">Student Name</th>
                <th class="text-left text-capitalize">Email</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(item, index) in students.results" :key="item.id">
                <td>
                  <b class="pr-2">{{ index + 1 }}</b> {{ item.first_name }}
                  {{ item.last_name }}
                </td>
                <td>{{ item.email }}</td>
              </tr>
            </tbody>
          </template>
        </v-simple-table>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="6" class="d-flex">
        <v-btn color="#10AFA7" class="text-capitalize" outlined>
          <v-icon class="pr-2" dense>mdi-plus-circle-outline</v-icon> Көбірек
          оқушылар</v-btn
        >
        <v-spacer></v-spacer>

        <v-dialog v-model="dialog" max-width="600px">
          <template #activator="{ on, attrs }">
            <v-btn
              color="#10AFA7"
              dark
              class="text-capitalize"
              v-bind="attrs"
              v-on="on"
            >
              Адамдарды шақыру
            </v-btn>
          </template>
          <v-card>
            <v-form @submit.prevent="inviteStudent">
              <v-card-title class="justify-center">
                <span class="headline">Көбірек оқушы қосу</span>
              </v-card-title>
              <v-card-text>
                <v-container>
                  <v-row>
                    <v-col cols="12">
                      <v-autocomplete
                        v-model="selectedStudents"
                        :disabled="isUpdating"
                        :items="searchStudents.results"
                        filled
                        chips
                        required
                        color="#10AFA7"
                        label="Адамдарды шақыру"
                        item-text="name"
                        item-value="name"
                        multiple
                      >
                        <template #selection="data">
                          <v-chip
                            v-bind="data.attrs"
                            :input-value="data.selected"
                            close
                            @click="data.select"
                            @click:close="remove(data.item)"
                          >
                            <v-avatar left>
                              <v-img :src="data.item.avatar"></v-img>
                            </v-avatar>
                            {{ data.item.first_name }} {{ data.item.last_name }}
                          </v-chip>
                        </template>
                        <template #item="data">
                          <template v-if="typeof data.item !== 'object'">
                            <v-list-item-content
                              v-text="data.item"
                            ></v-list-item-content>
                          </template>
                          <template v-else>
                            <v-list-item-avatar>
                              <img :src="data.item.avatar" />
                            </v-list-item-avatar>
                            <v-list-item-content>
                              <v-list-item-title
                                >{{ data.item.first_name }}
                                {{ data.item.last_name }}</v-list-item-title
                              >
                            </v-list-item-content>
                          </template>
                        </template>
                      </v-autocomplete>
                    </v-col>
                  </v-row>
                </v-container>
              </v-card-text>
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn
                  color="#10AFA7"
                  text
                  class="text-capitalize"
                  @click="dialog = false"
                >
                  Болдырмау
                </v-btn>
                <v-btn
                  :color="selectedStudents.length <= 0 ? '#EFEEEE' : '#10AFA7'"
                  :dark="selectedStudents.length > 0"
                  class="text-capitalize"
                  :disabled="selectedStudents.length <= 0"
                  type="submit"
                >
                  Шақыру
                </v-btn>
              </v-card-actions>
            </v-form>
          </v-card>
        </v-dialog>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  async asyncData({ $axios, params }) {
    try {
      const students = await $axios.$get(`classes/students/${params.id}/`)
      const searchStudents = await $axios.$get('accounts/student-list/', {
        params: { class: params.id },
      })
      return { searchStudents, students }
    } catch (err) {
      return {
        searchStudents: [],
        students: [],
      }
    }
  },
  data() {
    return {
      dialog: false,
      autoUpdate: true,
      isUpdating: false,
      selectedStudents: [],
      searchStudents: [],
      students: [],
      items: [],
    }
  },
  watch: {
    isUpdating(val) {
      if (val) {
        setTimeout(() => (this.isUpdating = false), 3000)
      }
    },
  },
  methods: {
    remove(item) {
      const index = this.selectedStudents.indexOf(item)
      if (index >= 0) this.selectedStudents.splice(index, 1)
    },
    async inviteStudent() {
      try {
        await this.$axios.$patch(`classes/class/${this.$route.params.id}/`, {
          students: this.selectedStudents.map((student) => student.id),
        })

        this.students = await this.$axios.$get(
          `classes/students/${this.$route.params.id}/`
        )

        this.searchStudents = await this.$axios.$get('accounts/student-list/', {
          params: { class: this.$route.params.id },
        })

        this.selectedStudents = []

        this.dialog = false
      } catch (err) {
        // eslint-disable-next-line no-console
        console.log(err)
      }
    },
  },
}
</script>
