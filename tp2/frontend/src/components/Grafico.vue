<template>
  <div class="container">
    <div v-if="grafico === 1">
      <h3>Capital de mercado en USD</h3>
      <GChart type="ColumnChart" :data="capitalDeMercadoData" />
    </div>
    <div v-else-if="grafico === 2">
      <h3 class="mb-5">Volumen de tradeo de las últimas 24hs en USD</h3>
      <GChart
        class="my-3"
        :settings="{packages: ['bar']}"
        :data="volumenDeTradeoUltimas24hsData"
        :options="chartOptions"
        :createChart="(el, google) => new google.charts.Bar(el)"
        @ready="onChartReady"
      />
    </div>
  </div>
</template>

<script>
import { GChart } from "vue-google-charts";
import axios from "axios";

export default {
  name: "Grafico",
  components: {
    GChart
  },
  props: {
    grafico: Number
  },
  data: function() {
    return {
      token: "",
      capitalDeMercadoData: [["Criptomoneda", "Capital"]],
      volumenDeTradeoUltimas24hsData: [["Criptomoneda", "Volumen de tradeo"]],
      chartsLib: null
    };
  },
  methods: {
    llamadaAStrapi: async function() {
      await axios
        .get("http://localhost:1337/criptocurrencies", {
          headers: {
            Authorization: `Bearer ${this.token}`
          }
        })
        .then(response => {
          let data = response.data.slice(response.data.length - 15);
          data.map(criptomoneda => {
            this.capitalDeMercadoData.push([
              criptomoneda.symbol,
              criptomoneda.marketCap
            ]);
            this.volumenDeTradeoUltimas24hsData.push([
              criptomoneda.symbol,
              criptomoneda.volume
            ]);
          });
        });
    },
    onChartReady(chart, google) {
      this.chartsLib = google;
    }
  },
  computed: {
    chartOptions() {
      if (!this.chartsLib) return null;
      return this.chartsLib.charts.Bar.convertOptions({
        bars: "horizontal",
        hAxis: { format: "decimal" },
        height: 400,
        colors: ["#1b9e77"]
      });
    }
  },
  async mounted() {
    await axios
      .post("http://localhost:1337/auth/local", {
        identifier: "admin@gmail.com",
        password: "8c^#2T4!@!m4bS8C@3C995CNh5QVXH$@#R*J92vd9z4S4X"
      })
      .then(response => {
        this.token = response.data.jwt;
        this.llamadaAStrapi();
      });
  }
};
</script>

<style scoped>
</style>