<template>
  <div id="app">
    <div id="contenido">
      <Cabecera />
      <main role="main" class="container mt-3">
        <div class="row">
          <BarraLateral
            @cambiarComponente="cambiarComponente"
            @cambiarGrafico="cambiarGrafico"
            :grafico="grafico"
          />
          <div class="col-9">
            <div class="container">
              <Principal v-if="componente === 'principal'" />
              <CargarDatos v-if="componente === 'cargar'" />
              <VisualizarDatos
                v-if="componente === 'visualizar'"
                :grafico="grafico"
                :visualizar="visualizar"
              />
            </div>
          </div>
        </div>
      </main>
    </div>
    <Footer />
  </div>
</template>

<script>
import Cabecera from "./components/Cabecera";
import Footer from "./components/Footer";
import BarraLateral from "./components/BarraLateral";
import Principal from "./components/Principal";
import CargarDatos from "./components/CargarDatos";
import VisualizarDatos from "./components/VisualizarDatos";

export default {
  name: "App",
  components: {
    Cabecera,
    Footer,
    BarraLateral,
    Principal,
    CargarDatos,
    VisualizarDatos
  },
  data: function() {
    return {
      componente: "principal",
      visualizar: false,
      grafico: 2
    };
  },
  methods: {
    cambiarComponente: function(componente, visualizar) {
      this.componente = componente;
      if (visualizar) this.visualizar = visualizar;
    },
    cambiarGrafico: function(grafico) {
      this.grafico = grafico;
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  position: relative;
  min-height: 100vh;
}
#contenido {
  padding-bottom: 5rem;
}
a,
a:visited,
a:hover {
  color: #42b983;
}
a:hover {
  font-weight: bold;
}
</style>
