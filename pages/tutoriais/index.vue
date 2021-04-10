<template>
  <div id="atividades">
    <p class="text-h3">
      Buscar tutorial
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
    <ImagesStatus
      :atividades-filtradas="atividadesFiltradas"
      :search-term="searchTerm"
    />
    <v-card
      v-for="atividade in atividadesFiltradas"
      :key="atividade.title"
      class="mt-2"
      to="atividade"
    >
      <v-img
        max-height="100"
        :src="atividade.image"
        alt="Imagem de um arquivo"
        gradient="to bottom, rgba(100,115,201,.33), rgba(25,32,72,.7)"
      />
      <v-card-title>{{ atividade.title }}</v-card-title>
      <v-card-text>{{ atividade.description }}</v-card-text>
    </v-card>
    <ErrorDialog
      :error-message="errorMessage"
      @setErrorMessage="setErrorMessage"
    />
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
  },
  methods: {
    setErrorMessage (content) {
      this.errorMessage = content
    }
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
