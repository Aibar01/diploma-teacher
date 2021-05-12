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
                <v-col v-if="item.title == 'Howework'" cols="12">
                  <v-text-field
                    v-model="newItem.due_date"
                    outlined
                    label="Due to"
                    placeholder="24 March 2021, 00:00"
                    required
                  ></v-text-field>
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
      newItem: {
        title: '',
        description: '',
        uploaded_file: '',
        due_date: '',
      },
    }
  },
  methods: {
    async createItem(type) {
      type = type.toLowerCase()

      const config = {
        headers: { 'content-type': 'multipart/form-data' },
      }
      const formData = new FormData()
      for (const data in this.newItem) {
        formData.append(data, this.newItem[data])
      }

      formData.append('scratch_class', this.$route.params.id)

      try {
        await this.$axios.$post(`classes/${type}/`, formData, config)
        this.classwork = await this.$axios.$get(
          `classes/classwork/${this.$route.params.id}/`
        )
        this.dialog = false
      } catch (err) {
        // eslint-disable-next-line no-console
        console.log(err)
      }
    },
  },
}
</script>
