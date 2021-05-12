<template>
  <v-container>
    <v-row>
      <v-col cols="9">
        <v-expansion-panels>
          <v-expansion-panel v-for="item in items.results" :key="item.id">
            <v-expansion-panel-header disable-icon-rotate>
              {{ item.question }}
              <template #actions>
                <v-icon
                  v-if="item.is_active"
                  @click="item.is_active = !item.is_active"
                >
                  mdi-minus-circle-outline
                </v-icon>
                <v-icon v-else @click="item.is_active = !item.is_active">
                  mdi-plus-circle-outline
                </v-icon>
              </template>
            </v-expansion-panel-header>
            <v-expansion-panel-content>
              {{ item.answer }}
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
                  <v-form @submit.prevent="createQuestion">
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
                              v-model="question.name"
                              label="Your name"
                              placeholder="Enter your name"
                              outlined
                              required
                            ></v-text-field>
                          </v-col>
                          <v-col cols="12" class="pb-0">
                            <v-textarea
                              v-model="question.problem"
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
                        :color="
                          question.name && question.problem
                            ? '#10AFA7'
                            : '#EFEEEE'
                        "
                        class="mx-auto text-capitalize"
                        dark
                        type="submit"
                      >
                        Send
                      </v-btn>
                    </v-card-actions>
                  </v-form>
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
  layout: 'about',
  async asyncData({ $axios }) {
    try {
      const items = await $axios.$get('faq/faq/')
      return { items }
    } catch (err) {
      return { items: [] }
    }
  },
  data() {
    return {
      dialog: false,
      items: [],
      question: {
        name: '',
        problem: '',
      },
    }
  },
  methods: {
    async createQuestion() {
      try {
        await this.$axios.$post('faq/problem/', {
          ...this.question,
        })
        this.dialog = false
      } catch (err) {
        // eslint-disable-next-line no-console
        console.log(err)
      }
    },
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
