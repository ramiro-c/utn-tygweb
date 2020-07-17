<template>
  <aside class="col-3">
    <ul class="list-group list-group-flush">
      <li class="list-group-item">
        <a href="#" @click.prevent="cambiarComponente('cargar')">Cargar datos</a>
      </li>
      <li class="list-group-item">
        <a href="#" @click.prevent="cambiarGrafico('visualizar')">Visualizar datos</a>
      </li>
    </ul>
  </aside>
</template>

<script>
export default {
  name: "BarraLateral",
  props: {
    grafico: Number
  },
  methods: {
    cambiarComponente: function(componente) {
      let visualizar = false;
      if (componente === "cargar") {
        visualizar = true;
      }
      this.$emit("cambiarComponente", componente, visualizar);
    },
    cambiarGrafico: function(componente) {
      this.cambiarComponente(componente);
      this.$emit("cambiarGrafico", this.grafico === 1 ? 2 : 1);
    }
  }
};
</script>
