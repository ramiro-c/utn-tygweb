<template>
  <div class="container">
    <p v-if="!visualizar">Debe hacer click en 'Cargar datos' en primer lugar</p>
    <Grafico v-else-if="visualizar" :grafico="grafico" />
  </div>
</template>

<script>
import Grafico from "./Grafico";

export default {
  name: "VisualizarDatos",
  props: {
    grafico: Number,
    visualizar: Boolean
  },
  components: {
    Grafico
  }
};
</script>
