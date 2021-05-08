<template>
  <div class="mt-10 pl-5">
    <v-card elevation="0" max-width="900">
      <v-card-title class="pb-0">
        <v-list-item class="pl-0 grow">
          <v-list-item-avatar color="#10AFA7">
            <img
              alt="Avatar"
              src="https://avatars0.githubusercontent.com/u/9064066?v=4&s=460"
            />
          </v-list-item-avatar>

          <v-list-item-content>
            <div class="d-flex">
              <div>
                <v-text-field
                  label="Announce something to class"
                ></v-text-field>
              </div>
            </div>
          </v-list-item-content>
        </v-list-item>
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
      <v-card-title>
        <v-list-item class="pl-0 grow">
          <v-list-item-avatar color="#10AFA7">
            <img
              alt="Avatar"
              src="https://avatars0.githubusercontent.com/u/9064066?v=4&s=460"
            />
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
                        <v-card-text>This action is unrecoveravle.</v-card-text>
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

      <v-card-text class="font-weight-bold">
        {{ data.content }}
      </v-card-text>
    </v-card>
  </div>
</template>

<script>
export default {
  layout: 'private',
  data() {
    return {
      dialog: false,
      data: {
        title: 'Aidyn Jomart',
        content: 'Welcome everyone to this NEW class of Scratch!',
        date: '12 Mar 2021 at 12:01',
      },
      items: [
        { title: 'Move to top' },
        { title: 'Copy link' },
        { title: 'Edit' },
        { title: 'Delete' },
      ],
    }
  },
}
</script>
