<template>
  <v-app dark>
    <v-navigation-drawer
      v-model="drawer"
      app
    >
      <v-list subheader>
        <v-subheader>Users in room:</v-subheader>

        <v-list-item
          v-for="({name, id}, index) in users"
          :key="index"
          @click.prevent
        >
          <v-list-item-content>
            <v-list-item-title v-text="name" />
          </v-list-item-content>

          <v-list-item-icon>
            <v-icon
              :color="id === user.id ? 'primary' : 'grey'"
            >mdi-account-circle-outline</v-icon>
          </v-list-item-icon>

        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar
      app
    >
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-toolbar-title>
        Room
        <v-chip color="blue">{{ user.room }}</v-chip>
      </v-toolbar-title>

      <v-spacer />

      <v-btn
        icon
        class="mx-1"
        @click="exit"
      >
        <v-icon>mdi-exit-to-app</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <v-container fluid style="height: 100%">
        <Nuxt />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import {mapState} from "vuex";

export default {
  name: 'DefaultLayout',
  data () {
    return {
      drawer: true,
    }
  },
  computed: {
    ...mapState([
      'user',
      'users'
    ])
  },
  created() {
    console.log('JOIN ROOM1')
  },
  methods: {
    exit() {
      console.log('exit')
    }
  }
}
</script>
