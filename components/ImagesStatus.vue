<template>
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
</template>
<script>
export default {
  props: {
    atividadesFiltradas: {
      type: Array,
      default: () => []
    },
    searchTerm: {
      type: String,
      default: () => ''
    }
  }
}
</script>
