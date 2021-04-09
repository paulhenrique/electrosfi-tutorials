<template>
  <div id="colaborate">
    <p class="text-h3">
      Bem vindo!
    </p>
    <p class="text-subtitle">
      Este ambiente foi desenvolvido para divulgar e facilitar o uso do
      ElectrosFI em aplicações educacionais
    </p>
    <p class="mt-6">
      Aqui você encontrará alguns tutoriais que permitirão o uso do ElectrosFI
      em sala de aula como recurso didático para o ensino de Ondulatória, Óptica
      e Eletromagnetismo.
    </p>
    <p class="mt-6">
      Tem interesse em colaborar para esse projeto?
      <router-link to="/colaborar">
        Clique aqui e saiba como.
      </router-link>
    </p>

    <v-row class="mt-12">
      <v-spacer />
      <v-btn large rounded color="cyan" to="/tutoriais" dark>
        Voltar aos Tutoriais
        <v-icon right>
          mdi-chevron-right
        </v-icon>
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
