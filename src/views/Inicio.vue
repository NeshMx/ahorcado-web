<template>
  <div class="inicio">
    <b-jumbotron bg-variant="dark" text-variant="white" header="Juego del Ahorcado" lead="Por: Alex Huerta - 14141111">
      <p>Para más información visita mi repositorio de GitHub</p>
      <b-btn variant="primary" href="https://github.com/NeshMx/ahorcado-web" target="_blank">
        Más información
      </b-btn>
    </b-jumbotron>
    <ahorcado></ahorcado>
  </div>
</template>

<script>
import Ahorcado from "@/components/Ahorcado.vue";

export default {
  name: "inicio",
  components: {
    Ahorcado
  }
};
</script>
