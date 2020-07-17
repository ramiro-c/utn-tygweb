<template>
  <div class="container">
    <h3 class="titulo">Criptomonedas</h3>
    <div class="row">
      <div class="card col-md-5" v-for="criptomoneda in criptomonedas" :key="criptomoneda.symbol">
        <div class="card-content">
          <div class="img">
            <img :src="criptomoneda.iconUrl" alt />
          </div>
          <h4 class="name">{{criptomoneda.name}}</h4>
          <p class="symbol">{{criptomoneda.symbol}}</p>
          <div class="datos">
            <p>Capital en mercado: {{criptomoneda.marketCap}} USD</p>
            <p>Volumen de tradeo (ultimas 24hs): {{criptomoneda.volume}} USD</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "CargarDatos",
  data: function() {
    return {
      token: "",
      criptomonedas: []
    };
  },
  methods: {
    llamarAPI: async function() {
      await axios
        .get(
          "https://api.coinranking.com/v1/public/coins?base=USD&ids=2,3,4,5,7,8,12,13,24,34,45,46,57,59,69"
        )
        .then(response => {
          this.enviarDatosAStrapi(response.data.data);
        });
    },
    enviarDatosAStrapi: function(data) {
      data.coins.map(coin => {
        this.criptomonedas.push(coin);
        const { symbol, marketCap, volume } = coin;
        const dataCripto = { symbol, marketCap, volume };
        axios
          .post("http://localhost:1337/criptocurrencies", dataCripto, {
            headers: {
              Authorization: `Bearer ${this.token}`
            }
          })
          .catch(error => console.error(error));
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
        this.llamarAPI();
      });
  }
};
</script>

<style scoped>
.titulo {
  text-align: center;
  display: block;
  margin: auto;
}
.datos p {
  margin: 0;
}
.datos p:last-child {
  margin-bottom: 15px;
}
.datos {
  text-transform: none;
  font-weight: 300;
  font-size: 13px;
  margin: 10px 0;
  padding: 0 20px;
}
.datos p:first-child {
  margin-top: 5px;
}
.card {
  width: auto;
  text-transform: uppercase;
  text-align: center;
  margin: 10px auto;
  border: none;
  background-color: #fafafa;
}
.img {
  width: 150px;
  height: 150px;
  margin: 45px auto 0;
  border-radius: 50%;
  overflow: hidden;
}
.img img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
.name {
  font-weight: 500;
  font-size: 20px;
  color: black;
  margin-top: 25px;
}
.symbol {
  color: #42b983;
  font-weight: 400;
  font-size: 13px;
}
</style>