<template>
  <section>
    <p>Mis datos:</p>
    <ul>
      <li>- Nombre: Cerdá, Ramiro</li>
      <li>- Legajo: 30103</li>
    </ul>
    <p>
      API utilizada para el trabajo:
      <a
        href="https://coinranking.com/page/cryptocurrency-api"
        target="_blank"
      >Coinranking</a>
    </p>
    <p>Tecnologias:</p>
    <ul>
      <li>- Vue JS</li>
      <li>- Strapi</li>
    </ul>
  </section>
</template>

<script>
export default {
  name: "Principal"
};
</script>

<style scoped>
section p {
  margin: 5px 0;
}
section ul {
  padding-left: 15px;
  margin: 0;
}
section ul li {
  list-style: none;
}
</style>