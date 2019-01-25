<template>
  <v-app>
    <v-toolbar app>
      <v-toolbar-title class="headline text-uppercase">
        <span>Vuetify</span>
        <span class="font-weight-light">MATERIAL DESIGN</span>
      </v-toolbar-title>
    </v-toolbar>

    <v-content>
      <TestCaseList />
    </v-content>
  </v-app>
</template>

<script>
import TestCaseList from './components/TestCaseList'

export default {
  name: 'App',
  components: {
    TestCaseList
  },
  data () {
    return {
      //
    }
  }
}
</script>
