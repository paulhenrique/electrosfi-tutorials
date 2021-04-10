<template>
  <div id="atividades">
    <p class="text-h3">
      Buscar atividade
    </p>
    <p class="text-subtitle">
      Digite um termo para encontrar alguma atividade
    </p>
    <v-text-field
      v-model="searchTerm"
      color="cyan"
      filled
      :error="statusBusca"
      :hint="message"
      label="Digite aqui um termo para busca"
    />
    <center>
      <img
        v-if="searchTerm === ''"
        class="responsiveImg"
        src="~/assets/img/search.svg"
        alt="Figura de Busca"
      >
      <img
        v-if="atividadesFiltradas.length === 0 && searchTerm !== ''"
        class="responsiveImg"
        src="~/assets/img/void.svg"
        alt="Figura de Busca"
      >
    </center>
    <v-card v-for="atividade in atividadesFiltradas" :key="atividade.title">
      <v-card-title>{{ atividade.title }}</v-card-title>
    </v-card>
    <v-dialog v-model="error" max-width="300">
      <v-card>
        <v-card-title>Algo de errado aconteceu</v-card-title>
        <v-card-text>
          Isso é possivelmente um problema com o nosso servidor, por favor tente
          mais tarde.
        </v-card-text>
        <v-card-actions>
          <v-spacer />
          <v-btn dark large color="cyan" @click="errorMessage = ''">
            Entendi!
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>
<script>
export default {
  data () {
    return {
      atividades: [],
      searchTerm: '',
      errorMessage: ''
    }
  },
  computed: {
    error: {
      get () {
        return this.errorMessage !== ''
      },
      set () {
        this.errorMessage = ''
      }
    },
    statusBusca () {
      return this.atividadesFiltradas.length === 0 && this.searchTerm !== ''
    },
    message () {
      if (this.atividadesFiltradas.length === 0 && this.searchTerm !== '') {
        return 'Termo não encontrado'
      } else {
        return ''
      }
    },
    atividadesFiltradas () {
      if (this.searchTerm === '') {
        return []
      }
      return this.atividades.filter((el) => {
        const string = el.title.toLowerCase() + el.description.toLowerCase()
        const palavras = this.searchTerm.toLowerCase().split(' ')
        let search = 0
        palavras.forEach((palavra) => {
          search = string.toLowerCase().split(palavra)
        })

        return search.length > 1
      })
    }
  },
  mounted () {
    fetch('/atividades.json')
      .then((data) => {
        if (data.ok) {
          return data.json()
        } else {
          throw new Error('Algo de errado aconteceu na consulta dos dados')
        }
      })
      .then((response) => {
        this.atividades = response
      })
      .catch((err) => {
        this.errorMessage = err.message
      })
  }
}
</script>
<style lang="scss">
#colaborateImg {
  min-height: 100vh;
  user-select: none;
  position: fixed;
  left: 0;
  width: 30vw;
  top: 0;
}
.responsiveImg {
  max-width: 80%;
  margin: auto;
}
</style>
