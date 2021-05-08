<template>
  <v-container fluid>
    <v-row>
      <v-col cols="6">
        <v-simple-table>
          <template #default>
            <thead class="background-color:#999999 !important">
              <tr>
                <th class="text-left text-capitalize">Student Name</th>
                <th class="text-left text-capitalize">Email</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(item, index) in students" :key="item.name">
                <td>
                  <b class="pr-2">{{ index + 1 }}</b> {{ item.name }}
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
          <v-icon class="pr-2" dense>mdi-plus-circle-outline</v-icon> More
          students</v-btn
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
              Invite student
            </v-btn>
          </template>
          <v-card>
            <v-card-title class="justify-center">
              <span class="headline">Invitation</span>
            </v-card-title>
            <v-card-text>
              <v-container>
                <v-row>
                  <v-col cols="12">
                    <v-text-field label="Email*" required></v-text-field>
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
                Cancel
              </v-btn>
              <v-btn
                color="#10AFA7"
                dark
                class="text-capitalize"
                @click="dialog = false"
              >
                Invite
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      dialog: false,
      students: [
        {
          name: 'Aibar Bekkozhayev Yogurt',
          email: 'asd@gmail.com',
        },
        {
          name: 'Aibar Bekkozhayev cream sandwich',
          email: 'asd@gmail.com',
        },
        {
          name: 'Aibar Bekkozhayev',
          email: 'asd@gmail.com',
        },
        {
          name: 'Aibar Bekkozhayev',
          email: 'asd@gmail.com',
        },
        {
          name: 'Aibar Bekkozhayev',
          email: 'asd@gmail.com',
        },
        {
          name: 'Aibar Bekkozhayev bean',
          email: 'asd@gmail.com',
        },
        {
          name: 'Aibar Bekkozhayev',
          email: 'asd@gmail.com',
        },
        {
          name: 'Aibar Bekkozhayev',
          email: 'asd@gmail.com',
        },
        {
          name: 'Aibar Bekkozhayev',
          email: 'asd@gmail.com',
        },
        {
          name: 'Aibar Bekkozhayev',
          email: 'asd@gmail.com',
        },
      ],
    }
  },
}
</script>
