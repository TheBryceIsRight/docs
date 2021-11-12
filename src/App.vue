<template>
  <v-app>
    <v-app-bar
      color="#4B466F"
      dark
    >
      <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>


      <v-toolbar-title>Documentation</v-toolbar-title>

      <v-spacer></v-spacer>

      <v-btn icon>
        <v-icon>mdi-heart</v-icon>
      </v-btn>

      <v-btn icon>
        <v-icon>mdi-magnify</v-icon>
      </v-btn>

      <v-menu
        left
        bottom
      >
        <template v-slot:activator="{ on, attrs }">
          <v-btn
            icon
            v-bind="attrs"
            v-on="on"
          >
            <v-icon>mdi-dots-vertical</v-icon>
          </v-btn>
        </template>

        <v-list>
          <v-list-item
            v-for="n in 5"
            :key="n"
            @click="() => {}"
          >
            <v-list-item-title>Option {{ n }}</v-list-item-title>
          </v-list-item>
        </v-list>
      </v-menu>
    </v-app-bar>
    <v-main>
      
    
     <v-navigation-drawer
      v-model="drawer"
      absolute
      clipped-left
      temporary
      width=550px
    >
      <v-list>
      <v-list-item>
        <v-list-item-icon>
          <v-icon>mdi-home</v-icon>
        </v-list-item-icon>

        <v-list-item-title>Home</v-list-item-title>
      </v-list-item>

      <v-list-group
        :value="true"
        prepend-icon="mdi-book-open-page-variant "
      >
        <template v-slot:activator>
          <v-list-item-title>User Guide</v-list-item-title>
        </template>



        <v-list-group
          :value="false"
          no-action
          sub-group
        >
          <template v-slot:activator>
            <v-list-item-content>
              <v-list-item-title>Onboarding</v-list-item-title>
            </v-list-item-content>
          </template>

          <v-list-item
            v-for="([title, icon], i) in training"
            :key="i"
            link
          >
            <v-list-item-title v-text="title"></v-list-item-title>

            <v-list-item-icon>
              <v-icon v-text="icon"></v-icon>
            </v-list-item-icon>
          </v-list-item>
        </v-list-group>

                <v-list-group
          :value="false"
          no-action
          sub-group
        >
          <template v-slot:activator>
            <v-list-item-content>
              <v-list-item-title>Administration</v-list-item-title>
            </v-list-item-content>
          </template>

          <v-list-item
            v-for="([title, icon], i) in administration"
            :key="i"
            link
          >
            <v-list-item-title v-text="title"></v-list-item-title>

            <v-list-item-icon>
              <v-icon v-text="icon"></v-icon>
            </v-list-item-icon>
          </v-list-item>
        </v-list-group>
        
        <v-list-group
          :value="true"
          no-action
          sub-group
        >
          <template v-slot:activator>
            <v-list-item-content>
              <v-list-item-title>Executions & Orchestrations</v-list-item-title>
            </v-list-item-content>
          </template>

          <v-list-item
            v-for="([title, icon], i) in admins"
            :key="i"
            link
          >
            <v-list-item-title v-text="title"></v-list-item-title>

            <v-list-item-icon>
              <v-icon v-text="icon"></v-icon>
            </v-list-item-icon>
          </v-list-item>
        </v-list-group>

        <v-list-group
          no-action
          sub-group
        >
          <template v-slot:activator>
            <v-list-item-content>
              <v-list-item-title>Actions</v-list-item-title>
            </v-list-item-content>
          </template>

          <v-list-item
            v-for="([title, icon], i) in cruds"
            :key="i"
            link
          >
            <v-list-item-title v-text="title"></v-list-item-title>

            <v-list-item-icon>
              <v-icon v-text="icon"></v-icon>
            </v-list-item-icon>
          </v-list-item>
        </v-list-group>
      </v-list-group>
    </v-list>
    </v-navigation-drawer>
    <v-container>
       <v-container>
    <v-timeline>
    <v-timeline-item
      v-for="(year, i) in years"
      :key="i"
      :color="year.color"
      small
    >
      <template v-slot:opposite>
        <span
          :class="`headline font-weight-bold ${year.color}--text`"
          v-text="year.year"
        ></span>
      </template>
      <div class="py-4">
        <h2 :class="`headline font-weight-light mb-4 ${year.color}--text`">
          {{documents[i].name}}
        </h2>
        <p>
          {{documents[i].description}}
        </p>
      </div>
    </v-timeline-item>
  </v-timeline>
  </v-container>
</v-container>
    
      <router-view/>

    </v-main>
  </v-app>
</template>

<script>
import axios from 'axios'
  export default {
    name: 'App',
    data: () => ({
        selected: [2],
        years: [
          {
            color: 'cyan',
            year: '2018 Q2',
          },
          {
            color: 'green',
            year: '2018 Q4',
          },
          {
            color: 'pink',
            year: '2019 Q2',
          },
          {
            color: 'amber',
            year: '2019 Q4',
          },
          {
            color: 'orange',
            year: '2020 Q3',
          },
        ],
        items: [
          {
            action: '15 min',
            headline: 'Wednesday at 12:57',
            subtitle: `Resolved an issue where email notification was not received after certain orchestration executions.`,
            title: "What's New in Version 5.0.16?",
          },
          {
            action: '2 hr',
            headline: 'November 03, 2021 07:00',
            subtitle: `Resolved an issue where certain orchestration APIs were not triggering the start of an orchestration`,
            title: "What's New in Version 5.0.15?",
          },
          {
            action: '6 hr',
            headline: 'October 25, 2021 12:23',
            subtitle: 'Resolved a performance issue on certain popups throughout the application.',
            title: "What's New in Version 5.0.14?",
          },
          {
            action: '12 hr',
            headline: 'October 12, 2021 09:22',
            subtitle: 'Resolved a Slider View display issue occurring in certain tests.',
            title: "What's New in Version 5.0.13?",
          },
          {
            action: '18hr',
            headline: 'October 08, 2021 08:28',
            subtitle: 'Obfuscated passwords used in site authentication test cases in the Slider View.',
            title: "What's New in Version 5.0.12?",
          },
        ],
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

    watch: {
      group () {
        this.drawer = false
      },
    },

  }
</script>
