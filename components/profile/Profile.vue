<template>
  <div>
    <v-card>
      <v-img
        v-if="$auth.user.cover_image"
        max-height="224"
        :src="$auth.user.cover_image"
      >
      </v-img>
      <v-img
        v-else
        max-height="224"
        src="https://coolbackgrounds.io/images/backgrounds/index/sea-edge-79ab30e2.png"
      >
      </v-img>
    </v-card>
    <v-container>
      <v-row>
        <v-col cols="2">
          <v-card
            d-flex
            justify="center"
            align="center"
            class="mx-auto my-12"
            max-width="300"
            elevation="0"
            style="position: absolute; left: 100px; top: 70px"
          >
            <div id="avatar" class="pt-10 px-10">
              <v-avatar size="120">
                <img
                  v-if="$auth.user.avatar"
                  alt="user"
                  :src="$auth.user.avatar"
                />
                <img
                  v-else
                  alt="user"
                  src="https://randomuser.me/api/portraits/women/81.jpg"
                />
              </v-avatar>
              <v-card-subtitle class="title black--text pb-0"
                >{{ $auth.user.first_name }}
                {{ $auth.user.last_name }}</v-card-subtitle
              >
              <v-card-subtitle v-if="$auth.user.user_type" class="pt-2"
                >Мұғалым</v-card-subtitle
              >
              <v-card-subtitle v-else class="pt-2">Оқушы</v-card-subtitle>
              <v-divider></v-divider>
              <v-card-text d-flex align="start">
                {{ $auth.user.bio }}
              </v-card-text>
              <v-card-text d-flex align="center">
                <v-btn
                  color="#10AFA7"
                  class="text-capitalize"
                  text
                  @click="$router.push('/profile/settings')"
                >
                  <strong> Профиль өзгерту </strong>
                </v-btn>
              </v-card-text>
            </div>
          </v-card>
        </v-col>

        <v-col cols="10">
          <Result />
        </v-col>
        <v-col cols="10" class="ml-auto">
          <TeacherProfileClassPreview />
        </v-col>
      </v-row>
      <v-row>
        <v-col>
          <TeacherSharedList />
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
import TeacherProfileClassPreview from './TeacherProfileClassPreview'
import TeacherSharedList from './TeacherSharedList'
import Result from './Result'
export default {
  components: {
    TeacherProfileClassPreview,
    TeacherSharedList,
    Result,
  },
}
</script>

<style scoped>
.v-main__wrap {
  background-color: #efeeee;
}
</style>
