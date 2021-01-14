<template>
  <div>
    <h1 :style="{ textDecoration: decoration}">Hello {{ name }}</h1>
    <input type="text" v-model="name">
    <br>
    <a :href="link">Link para o curso!</a>
  </div>
</template>

<script>
export default {
    data: () => ({
        name: 'Ivan',
        link: 'https://treinamento.vuejsbrasil.org',
        decoration: 'underline',
    })
}
</script>

<style>

</style>