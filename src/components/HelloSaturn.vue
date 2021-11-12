<template>
    <v-list two-line>
      <v-list-item-group
        v-model="selected"
        active-class="pink--text"
        multiple
      >
        <template v-for="(item, index) in documents">
          <v-list-item :key="documents[index].name">
            <template v-slot:default="{ active }">
              <v-list-item-content>
                <v-list-item-title v-text="documents[index].name"></v-list-item-title>

                <v-list-item-subtitle
                  class="text--primary"
                  v-text="item.headline"
                ></v-list-item-subtitle>

                <v-list-item-subtitle v-text="documents[index].description"></v-list-item-subtitle>
              </v-list-item-content>

              <v-list-item-action>
                <v-icon
                  v-if="!active"
                  color="grey lighten-1"
                >
                  mdi-star-outline
                </v-icon>

                <v-icon
                  v-else
                  color="yellow darken-3"
                >
                  mdi-star
                </v-icon>
              </v-list-item-action>
            </template>
          </v-list-item>

          <v-divider
            v-if="index < items.length - 1"
            :key="index"
          ></v-divider>
        </template>
      </v-list-item-group>
    </v-list>
</template>

<script>
import axios from 'axios'
  export default {
    name: 'article',
    data: () => ({
      selected: [2],
      documents: [],
      error: null,
      drawer: false,
      group: null,
      admins: [
        ['Orchestrations', 'mdi-account-multiple-outline'],
        ['Test Case Execution', 'mdi-cog-outline'],
      ],
      training: [
        ['Getting the most out of self paced onboarding & training', 'mdi-school'],
        ['Intro & Prerequisites for training', 'mdi-school'],
        ['Session 1 - Create a test & execute', 'mdi-school'],
        ['Session 2 - NLP Creation, debugging, & editing tests', 'mdi-school'],
        ['Session 3 - Page Objects & Orchestrations', 'mdi-school'],
        ['Session 4 - TDM, Settings, & Integrations', 'mdi-school'],
        ['Opening and formatting support tickets', 'mdi-school'],
        ['Escalating support tickets', 'mdi-school'],
      ],
      administration: [
        ['SSO Configurations', 'mdi-cog'],
        ['Product Limitations', 'mdi-cog'],
        ['List of Devices supported', 'mdi-cog'],
        ['How to add a new user to functionize (admin only)', 'mdi-cog'],
      ],
      cruds: [
        ['Create', 'mdi-plus-outline'],
        ['Read', 'mdi-file-outline'],
        ['Update', 'mdi-update'],
        ['Delete', 'mdi-delete'],
      ],
    }),
    async mounted () {
      try {
        const response = await axios.get('http://localhost:1337/documentations')
        this.documents = response.data
        console.log(this.documents);
      } catch (error) {
        this.error = error;
      }
    },


  }
</script>