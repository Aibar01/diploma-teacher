<template>
  <v-card
    class="pl-sm-0 pl-md-10 pt-sm-0 pt-md-10"
    elevation="0"
    max-width="30%"
  >
    <v-form>
      <v-container>
        <v-row>
          <v-col cols="12">
            <v-text-field label="First Name" outlined></v-text-field>
          </v-col>
          <v-col cols="12">
            <v-text-field label="Last Name" outlined></v-text-field>
          </v-col>
          <v-col cols="12">
            <v-select :items="items" label="Job position" outlined></v-select>
          </v-col>
          <v-col class="pb-0" cols="12">
            <v-textarea outlined label="Bio"></v-textarea>
          </v-col>
          <v-col class="pt-0 pb-10" cols="12">
            <v-btn class="font-weight-bold" color="#BDBDBD" dark> Save </v-btn>
          </v-col>
        </v-row>
        <v-row>
          <v-col class="pt-0" cols="12">
            <v-file-input
              prepend-icon="mdi-account-edit"
              label="Upload profile photo"
              outlined
            ></v-file-input>
          </v-col>
          <v-col class="pt-0" cols="12">
            <v-file-input
              prepend-icon="mdi-arrange-send-backward"
              label="Upload cover image"
              outlined
            ></v-file-input>
          </v-col>
          <v-col class="pt-0 pb-10" cols="12">
            <v-btn class="font-weight-bold" color="#BDBDBD" dark> Save </v-btn>
          </v-col>
        </v-row>
        <v-row>
          <v-col class="pb-0" cols="12">
            <v-text-field label="Email" outlined></v-text-field>
          </v-col>
          <v-col class="pt-0 pb-10" cols="12">
            <v-btn class="font-weight-bold" color="#BDBDBD" dark> Save </v-btn>
          </v-col>
        </v-row>
        <v-row>
          <v-col cols="12">
            <v-text-field label="New password" outlined></v-text-field>
          </v-col>
          <v-col class="pb-0" cols="12">
            <v-text-field label="Repeat new password" outlined></v-text-field>
          </v-col>
          <v-col class="pt-0 pb-10" cols="12">
            <v-btn class="font-weight-bold" color="#BDBDBD" dark> Save </v-btn>
          </v-col>
        </v-row>
        <v-row>
          <v-col class="pt-0" cols="12">
            <v-dialog v-model="dialog" persistent max-width="400">
              <template #activator="{ on, attrs }">
                <v-btn
                  class="font-weight-bold text-capitalize"
                  color="red"
                  dark
                  outlined
                  v-bind="attrs"
                  v-on="on"
                >
                  Delete account
                </v-btn>
              </template>
              <v-card d-flex justify="center" align="center">
                <v-card-title class="headline">
                  Are you sure you want to delete your account?
                </v-card-title>
                <v-card-text
                  >You will no longer have access to your classes or
                  participants. This action can’t be undone.</v-card-text
                >
                <v-card-actions>
                  <v-btn
                    width="100%"
                    class="font-weight-bold text-capitalize"
                    dark
                    color="red"
                    @click="dialog = false"
                  >
                    Delete
                  </v-btn>
                </v-card-actions>
                <v-card-actions>
                  <v-btn
                    width="100%"
                    class="font-weight-bold text-capitalize"
                    color="#BC3FF6"
                    outlined
                    @click="dialog = false"
                  >
                    Cancel
                  </v-btn>
                </v-card-actions>
              </v-card>
            </v-dialog>
          </v-col>
        </v-row>
      </v-container>
    </v-form>
  </v-card>
</template>

<script>
export default {
  layout(context) {
    return 'profile'
  },
  data: () => ({
    items: [
      'Programming teacher',
      'Programming teacher',
      'Programming teacher',
      'Programming teacher',
    ],
    dialog: false,
  }),
}
</script>
