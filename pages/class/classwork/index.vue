<template>
  <div class="mt-10 pl-5">
    <v-card class="pb-5" elevation="0" max-width="900">
      <v-card-title class="pb-0">
        <v-menu transition="slide-y-transition" offset-y bottom>
          <template #activator="{ on, attrs }">
            <v-btn class="py-4" color="#10AFA7" dark v-bind="attrs" v-on="on">
              <v-icon class="pr-2">mdi-plus-circle-outline</v-icon> Create
            </v-btn>
          </template>
          <v-list>
            <v-list-item v-for="(item, i) in items" :key="i">
              <v-dialog v-model="dialog" max-width="600px">
                <template #activator="{ on, attrs }">
                  <v-list-item-title v-bind="attrs" v-on="on">
                    <v-icon color="#10AFA7">{{ item.icon }}</v-icon>
                    {{ item.title }}
                  </v-list-item-title>
                </template>
                <v-card>
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
                            outlined
                            label="Title"
                            placeholder="Enter title"
                            required
                          ></v-text-field>
                        </v-col>
                        <v-col cols="12">
                          <v-textarea
                            outlined
                            name="input-7-4"
                            label="Description"
                            placeholder="(optional)"
                          ></v-textarea>
                        </v-col>
                        <v-col cols="12" class="d-flex">
                          <v-file-input
                            color="#10AFA7"
                            label="Add"
                            outlined
                          ></v-file-input>
                        </v-col>
                        <v-col cols="12">
                          <v-text-field
                            outlined
                            label="Points"
                            placeholder="100"
                            required
                          ></v-text-field>
                        </v-col>
                        <v-col cols="12">
                          <v-text-field
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
                    <v-btn
                      class="text-capitalize"
                      color="#10AFA7"
                      dark
                      @click="dialog = false"
                    >
                      Create lesson
                    </v-btn>
                    <v-btn class="text-capitalize" text @click="dialog = false">
                      Cancel
                    </v-btn>
                  </v-card-actions>
                </v-card>
              </v-dialog>
            </v-list-item>
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

    <v-card v-for="i in 4" :key="i" outlined max-width="500" class="mt-8">
      <nuxt-link to="classwork/1">
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
                  <v-list-item-title>{{ data.title }}</v-list-item-title>
                  <v-list-item-subtitle>{{ data.date }}</v-list-item-subtitle>
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
      </nuxt-link>
    </v-card>
  </div>
</template>

<script>
export default {
  layout: 'class',
  data() {
    return {
      dialog: false,
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
