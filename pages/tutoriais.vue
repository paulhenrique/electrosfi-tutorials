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
      filled
      label="Digite aqui um termo para busca"
    />
    <img
      v-if="searchTerm === ''"
      class="responsiveImg"
      src="~/assets/img/search.svg"
      alt="Figura de Busca"
    >
    <v-card v-for="atividade in atividadesFiltradas" :key="atividade.title">
      <v-card-title>{{ atividade.title }}</v-card-title>
    </v-card>
  </div>
</template>
<script>
export default {
  data () {
    return {
      atividades: [],
      searchTerm: '',
      erro: {
        status: false,
        message: ''
      }
    }
  },
  computed: {
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
        this.erro = {
          status: true,
          message: err.message
        }
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
  max-width: 100%;
}
</style>
