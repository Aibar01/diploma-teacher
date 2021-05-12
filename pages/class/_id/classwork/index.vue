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
            <v-btn class="py-4" color="#10AFA7" dark v-bind="attrs" v-on="on">
              <v-icon class="pr-2">mdi-plus-circle-outline</v-icon> Create
            </v-btn>
          </template>
          <v-list>
            <template v-for="(item, i) in items">
              <CardDialog :key="i" :item="item" :attrs="attrs" :on="on" />
            </template>
          </v-list>
        </v-menu>
      </v-card-title>
    </v-card>

    <v-card max-width="500" outlined>
      <v-card-text>
        <p class="headline text--primary">Communicate with your students</p>
        <p>
          <v-icon class="pr-2" color="black" x-small>mdi-circle</v-icon>Create
          and schedule announcements
        </p>
        <p>
          <v-icon class="pr-2" color="black" x-small>mdi-circle</v-icon>Respond
          to student posts
        </p>
      </v-card-text>
    </v-card>

    <v-card
      v-for="i in classwork.classwork"
      :key="i.id"
      outlined
      max-width="500"
      class="mt-8"
    >
      <nuxt-link :to="`classwork/${i}`">
        <v-card-title>
          <v-list-item class="pl-0 grow">
            <v-list-item-avatar color="#10AFA7">
              <span class="white--text headline">
                <v-icon dark>mdi-notebook</v-icon>
              </span>
            </v-list-item-avatar>

            <v-list-item-content>
              <div class="d-flex">
                <div>
                  <v-list-item-title>{{ i.title }}</v-list-item-title>
                  <v-list-item-subtitle>{{
                    $moment(new Date(+i.created_at * 1000)).format(
                      'D MMM YYYY, h:mm'
                    )
                  }}</v-list-item-subtitle>
                </div>
                <v-spacer></v-spacer>
                <v-menu offset-y>
                  <template #activator="{ on, attrs }">
                    <v-btn color="#C4C4C4" dark icon v-bind="attrs" v-on="on">
                      <v-icon dark> mdi-dots-horizontal </v-icon>
                    </v-btn>
                  </template>
                  <v-list>
                    <v-list-item>
                      <v-list-item-title>Edit</v-list-item-title>
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
                            Delete announcement?
                          </v-card-title>
                          <v-card-text
                            >This action is unrecoveravle.</v-card-text
                          >
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
                              @click="dialog = false"
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
      </nuxt-link>
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
  async asyncData({ $axios, params }) {
    try {
      const classwork = await $axios.$get(`classes/classwork/${params.id}/`)
      return {
        classwork,
      }
    } catch (err) {
      return { classwork: {} }
    }
  },
  data() {
    return {
      dialog: false,
      closeOn: true,
      classwork: {},
      data: {
        title: 'Lesson 1',
        content: 'Welcome everyone to this NEW class of Scratch!',
        date: '12 Mar 2021 at 12:01',
      },
      items: [
        { title: 'Lesson', icon: 'mdi-circle' },
        { title: 'Howework', icon: 'mdi-circle' },
        { title: 'Material', icon: 'mdi-circle' },
      ],
    }
  },
}
</script>
