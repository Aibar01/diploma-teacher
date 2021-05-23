<template>
  <v-card
    class="pl-sm-0 pl-md-10 pt-sm-0 pt-md-10"
    elevation="0"
    max-width="30%"
  >
    <v-container>
      <v-row>
        <v-col>
          <v-form @submit.prevent="editMainInfo">
            <v-col cols="12">
              <v-text-field
                v-model="user.first_name"
                label="Аты"
                outlined
              ></v-text-field>
            </v-col>
            <v-col cols="12">
              <v-text-field
                v-model="user.last_name"
                label="Тегі"
                outlined
              ></v-text-field>
            </v-col>
            <!-- <v-col cols="12">
            <v-select :items="items" label="Job position" outlined></v-select>
          </v-col> -->
            <v-col class="pb-0" cols="12">
              <v-textarea v-model="user.bio" outlined label="Био"></v-textarea>
            </v-col>
            <v-col class="pt-0 pb-10" cols="12">
              <v-btn
                class="font-weight-bold text-capitalize"
                color="#10AFA7"
                dark
                type="submit"
                elevation="0"
              >
                Сақтау
              </v-btn>
            </v-col>
          </v-form>
        </v-col>
      </v-row>
      <v-row>
        <v-col>
          <v-form @submit.prevent="UploadImages">
            <v-col class="pt-0" cols="12">
              <v-file-input
                v-model="user.avatar"
                prepend-icon="mdi-account-edit"
                label="Профиль фотосы"
                outlined
                accept="image/*"
              ></v-file-input>
            </v-col>
            <v-col class="pt-0" cols="12">
              <v-file-input
                v-model="user.cover_image"
                prepend-icon="mdi-arrange-send-backward"
                label="Артқы сурет"
                outlined
                accept="image/*"
              ></v-file-input>
            </v-col>
            <v-col class="pt-0 pb-10" cols="12">
              <v-btn
                class="font-weight-bold text-capitalize"
                color="#10AFA7"
                dark
                :disabled="user.avatar == '' && user.cover_image == ''"
                type="submit"
                elevation="0"
              >
                Сақтау
              </v-btn>
            </v-col>
          </v-form>
        </v-col>
      </v-row>
      <v-row>
        <v-col>
          <v-form>
            <v-col class="pb-0" cols="12">
              <v-text-field
                v-model="user.email"
                label="Email"
                outlined
              ></v-text-field>
            </v-col>
            <v-col class="pt-0 pb-10" cols="12">
              <v-btn
                elevation="0"
                class="font-weight-bold"
                color="#BDBDBD"
                disabled
              >
                Сақтау
              </v-btn>
            </v-col>
          </v-form>
        </v-col>
      </v-row>
      <v-row>
        <v-col>
          <v-form>
            <v-col cols="12">
              <v-text-field
                v-model="password"
                label="New password"
                outlined
              ></v-text-field>
            </v-col>
            <v-col class="pb-0" cols="12">
              <v-text-field
                v-model="confirm_password"
                label="Repeat new password"
                outlined
              ></v-text-field>
            </v-col>
            <v-col class="pt-0 pb-10" cols="12">
              <v-btn
                type="submit"
                class="font-weight-bold text-capitalize"
                color="#10AFA7"
                dark
                elevation="0"
              >
                Сақтау
              </v-btn>
            </v-col>
          </v-form>
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
                Аккаунт жою
              </v-btn>
            </template>
            <v-card d-flex justify="center" align="center">
              <v-card-title class="headline">
                Сіз аккаунт жоюға расында сенімдімісіз бе?
              </v-card-title>
              <v-card-text
                >Бұдан кейін сіз сабақтар мен материалдарды көре алмайсыз. Бұл
                қайтарылмайтын әрекет.
              </v-card-text>
              <v-card-actions>
                <v-btn
                  width="100%"
                  class="font-weight-bold text-capitalize"
                  dark
                  color="red"
                  @click="dialog = false"
                >
                  Жою
                </v-btn>
              </v-card-actions>
              <v-card-actions>
                <v-btn
                  width="100%"
                  class="font-weight-bold text-capitalize"
                  color="#10AFA7"
                  outlined
                  @click="dialog = false"
                >
                  Артқа
                </v-btn>
              </v-card-actions>
            </v-card>
          </v-dialog>
        </v-col>
      </v-row>
    </v-container>
  </v-card>
</template>

<script>
export default {
  layout: 'profile',
  midlleware: ['auth'],
  data: () => ({
    preview: '',
    items: [
      'Programming teacher',
      'Programming teacher',
      'Programming teacher',
      'Programming teacher',
    ],
    dialog: false,
    user: {},
    passoword: '',
    confirm_password: '',
  }),
  created() {
    this.user = this.$auth.user
  },
  methods: {
    async editMainInfo() {
      const editedMainInfo = {
        first_name: this.user.first_name,
        last_name: this.user.last_name,
        bio: this.user.bio,
      }

      const config = {
        headers: { 'content-type': 'multipart/form-data' },
      }
      const formData = new FormData()
      for (const data in editedMainInfo) {
        formData.append(data, editedMainInfo[data])
      }
      try {
        await this.$axios.$patch(`accounts/profile/`, formData, config)

        await this.$auth.fetchUser()
      } catch (e) {
        // eslint-disable-next-line no-console
        console.log(e)
      }
    },
    async UploadImages() {
      const editedImages = {
        avatar: this.user.avatar,
        cover_image: this.user.cover_image,
      }

      if (typeof editedImages.avatar === 'string') {
        delete editedImages.avatar
      }

      if (typeof editedImages.cover_image === 'string') {
        delete editedImages.cover_image
      }
      const config = {
        headers: { 'content-type': 'multipart/form-data' },
      }
      const formData = new FormData()
      for (const data in editedImages) {
        formData.append(data, editedImages[data])
      }
      try {
        await this.$axios.$patch(`accounts/profile/`, formData, config)
        await this.$auth.fetchUser()
      } catch (e) {
        // eslint-disable-next-line no-console
        console.log(e)
      }
    },
    async editPassword() {
      const editedPassword = {
        password: this.password,
        password1: this.confirm_password,
      }

      const config = {
        headers: { 'content-type': 'multipart/form-data' },
      }
      const formData = new FormData()
      for (const data in editedPassword) {
        formData.append(data, editedPassword[data])
      }
      try {
        await this.$axios.$patch(`accounts/change/password/`, formData, config)
        await this.$auth.fetchUser()
      } catch (e) {
        // eslint-disable-next-line no-console
        console.log(e)
      }
    },
  },
}
</script>
