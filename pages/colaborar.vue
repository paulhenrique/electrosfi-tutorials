<template>
  <div id="colaborate">
    <p class="text-h3">
      Colabore
    </p>
    <p class="text-subtitle">
      Quer colaborar com alguma atividade ou sugestão para o ElectrosFI?
    </p>
    <p class="mt-6">
      Envie um e-mail para
      <a href="mailto:electrosfi@gmail.com">electrosfi@gmail.com</a> com o
      assunto "Proposta de Atividade ElectrosFI - [Titulo-da-Atividade] -
      [Autor]". Busque seguir os mesmos padrões vistos aqui, lembre-se que a
      inserção de imagens e vídeos facilita muito a compreensão das atividades.
    </p>
    <v-row class="mt-12">
      <v-spacer />
      <v-btn large rounded color="purple" to="/tutoriais" dark>
        <v-icon left>
          mdi-chevron-left
        </v-icon>
        Voltar aos Tutoriais
      </v-btn>
    </v-row>
    <img
      id="colaborateImg"
      width="200"
      draggable="false"
      src="~/assets/img/colaborate.svg"
      alt=""
    >
  </div>
</template>
<style lang="scss">
#colaborateImg {
  min-height: 100vh;
  user-select: none;
  position: fixed;
  left: 0;
  width: 30vw;
  top: 0;
}
</style>
