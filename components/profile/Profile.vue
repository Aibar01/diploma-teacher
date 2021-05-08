<template>
  <div>
    <v-card>
      <v-img
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
                  alt="user"
                  src="https://img.freepik.com/free-photo/handsome-young-businessman-in-shirt-and-eyeglasses_85574-6228.jpg?size=626&ext=jpg"
                />
              </v-avatar>
              <v-card-subtitle class="title black--text pb-0"
                >Айбар Беккожаев</v-card-subtitle
              >
              <v-card-subtitle class="pt-2"
                >Programming мұғалым</v-card-subtitle
              >
              <v-divider></v-divider>
              <v-card-text d-flex align="start">
                I am 4 graded student at Haileyberry School. I have a big dream
                in my life - to become Super Cool Game Developer.
              </v-card-text>
              <v-card-text d-flex align="center">
                <v-btn
                  color="#10AFA7"
                  class="text-capitalize"
                  text
                  @click="$router.push('/profile/settings')"
                >
                  <strong> Edit Profile </strong>
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
