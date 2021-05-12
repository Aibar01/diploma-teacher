<template>
  <div id="app">
    <v-app id="inspire">
      <v-card :loading="isUpdating">
        <template #progress>
          <v-progress-linear
            absolute
            color="#10AFA7"
            height="4"
            indeterminate
          ></v-progress-linear>
        </template>
        <v-form>
          <v-container>
            <v-row>
              <v-col cols="12">
                <v-autocomplete
                  v-model="selectedStudents"
                  :disabled="isUpdating"
                  :items="searchStudents.results"
                  filled
                  chips
                  color="#10AFA7"
                  label="Invite students"
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
                      {{ data.item.name }}
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
        </v-form>
      </v-card>
    </v-app>
  </div>
</template>

<script>
export default {
  async asyncData({ $axios }) {
    try {
      const searchStudents = await $axios.$get('accounts/student-list/')
      return { searchStudents }
    } catch (err) {
      return { searchStudents: [] }
    }
  },
  data() {
    return {
      autoUpdate: true,
      isUpdating: false,
      selectedStudents: [],
      searchStudents: [],
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
      // eslint-disable-next-line no-console
      console.log(item)
      const index = this.selectedStudents.indexOf(item)
      if (index >= 0) this.selectedStudents.splice(index, 1)
    },
  },
}
</script>
