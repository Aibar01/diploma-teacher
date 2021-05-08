<template>
  <v-container>
    <v-row>
      <v-col cols="9">
        <v-expansion-panels>
          <v-expansion-panel v-for="(item, i) in items" :key="i">
            <v-expansion-panel-header disable-icon-rotate>
              {{ item.title }}
              <template #actions>
                <v-icon
                  v-if="item.is_active"
                  @click="item.is_active = !item.is_active"
                >
                  mdi-plus-circle-outline
                </v-icon>
                <v-icon v-else @click="item.is_active = !item.is_active">
                  mdi-minus-circle-outline
                </v-icon>
              </template>
            </v-expansion-panel-header>
            <v-expansion-panel-content>
              Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do
              eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut
              enim ad minim veniam, quis nostrud exercitation ullamco laboris
              nisi ut aliquip ex ea commodo consequat.
            </v-expansion-panel-content>
          </v-expansion-panel>
        </v-expansion-panels>
      </v-col>
      <v-col cols="3">
        <v-card class="mx-auto" color="#F8F8F8" max-width="400">
          <v-card-title>
            <span class="body-2 font-weight-light"
              >Didn’t find answers for your questions?</span
            >
          </v-card-title>

          <v-card-text>
            <v-row>
              <v-dialog v-model="dialog" max-width="500px">
                <template #activator="{ on, attrs }">
                  <v-btn
                    class="text-capitalize"
                    color="#10afa7"
                    text
                    dark
                    v-bind="attrs"
                    v-on="on"
                  >
                    Contact us
                  </v-btn>
                </template>
                <v-card d-flex justify="center" align="center">
                  <v-card-title class="py-10 px-12">
                    <span class="headline">
                      Tell us your problem and we will make anything to help
                      you!
                    </span>
                  </v-card-title>
                  <v-divider></v-divider>
                  <v-card-text class="pb-1">
                    <v-container>
                      <v-row>
                        <v-col cols="12">
                          <v-text-field
                            label="Your name"
                            placeholder="Enter your name"
                            outlined
                            required
                          ></v-text-field>
                        </v-col>
                        <v-col cols="12" class="pb-0">
                          <v-textarea
                            outlined
                            placeholder="Describe your problem"
                            label="How can we help you?"
                            required
                          ></v-textarea>
                        </v-col>
                      </v-row>
                    </v-container>
                  </v-card-text>
                  <v-card-actions class="pb-5">
                    <v-btn
                      color="#EFEEEE"
                      style="color: #b5b3b3"
                      class="mx-auto text-capitalize"
                      dark
                      @click="dialog = false"
                    >
                      Send
                    </v-btn>
                  </v-card-actions>
                </v-card>
              </v-dialog>
            </v-row>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  layout(context) {
    return 'about'
  },
  data() {
    return {
      dialog: false,
      items: [
        {
          title: 'Обучаете ли вы с нуля? Если я не из IT?',
          is_active: false,
        },
        {
          title:
            'Зачем платить за обучение, если в интернете можно найти всё бесплатно?',
          is_active: false,
        },
        {
          title: 'Какой график обучения? Получится ли совмещать его с работой?',
          is_active: false,
        },
        {
          title: 'Почему и как мы гарантируем трудоустройство?',
          is_active: false,
        },
      ],
    }
  },
}
</script>

<style scoped>
.v-expansion-panel::before {
  box-shadow: none;
}

.v-card__text {
  color: #10afa7 !important;
}
</style>
