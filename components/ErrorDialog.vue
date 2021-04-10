<template>
  <v-dialog v-model="error" max-width="300">
    <v-card>
      <v-card-title>Algo de errado aconteceu</v-card-title>
      <v-card-text>
        Isso é possivelmente um problema com o nosso servidor, por favor tente
        mais tarde.
      </v-card-text>
      <v-card-actions>
        <v-spacer />
        <v-btn dark large color="cyan" @click="atualizarErrorMessage('')">
          Entendi!
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>
<script>
export default {
  props: {
    errorMessage: {
      type: String,
      default: ''
    }
  },
  computed: {
    error: {
      get () {
        return this.errorMessage !== ''
      },
      set () {
        this.atualizarErrorMessage('')
      }
    }
  },
  methods: {
    atualizarErrorMessage (content) {
      this.$emit('setErrorMessage', content)
    }
  }
}
</script>
