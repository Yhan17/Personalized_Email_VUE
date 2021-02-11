<template>
  <div>
    <input v-model="nome"/>
    <h1>Cliente aqui</h1>
    <h2>Meu Componente</h2>
    <h2>{{nome}}</h2>
  </div>
</template>
<script>
export default {
  
  data: () => ({
    nome: "@teste"
  })
};
</script>
<style scoped>
h1 {
  text-align: center;
}
h2 {
  text-align: center;
}
</style>