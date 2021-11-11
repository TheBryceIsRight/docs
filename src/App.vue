<template>
  <v-app>
    <v-main>
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
    
     <v-navigation-drawer
      v-model="drawer"
      absolute
      bottom
      temporary
      width=45%
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
   
    
      <router-view/>
    </v-main>
  </v-app>
</template>

<script>
  export default {
    data: () => ({
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

    watch: {
      group () {
        this.drawer = false
      },
    },

  }
</script>
