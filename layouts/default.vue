<template>
  <v-app>
    <v-app-bar fixed app>
      <v-toolbar-title v-text="title" />
      <v-spacer />
      <v-tabs centered :color="colorTabs">
        <v-tab to="/">
          Boas vindas
        </v-tab>
        <v-tab to="/tutoriais">
          Tutoriais
        </v-tab>
        <v-tab to="/colaborar">
          Colaborar
        </v-tab>
      </v-tabs>
      <v-spacer />
      <v-btn icon light>
        <v-icon>mdi-information</v-icon>
      </v-btn>
    </v-app-bar>
    <v-main class="pt-12 mt-12">
      <v-container>
        <v-row justify="center">
          <v-col cols="5">
            <router-view />
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  data () {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: 'mdi-apps',
          title: 'Welcome',
          to: '/'
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'Inspire',
          to: '/inspire'
        }
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'ElectrosFI Tutorials'
    }
  },
  computed: {
    colorTabs () {
      const routes = [
        { rota: 'colaborar', color: 'purple' },
        { rota: 'index', color: 'orange' },
        { rota: 'tutoriais', color: 'cyan' },
        { rota: 'tutoriais-id', color: 'cyan' }
      ]
      let color = 'cyan'
      console.log(this.$route)
      if (this.$route.name) {
        const filredRoutes = routes.filter(el => el.rota === this.$route.name)
        color = filredRoutes.length > 0 ? filredRoutes[0].color : 'cyan'
      }
      return color
    }
  }
}
</script>
