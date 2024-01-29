<script>
import TheHeader from './components/TheHeader.vue'
export default {
  data() {
    return {
      dadosGitHub: null
    };
  },
  methods: {
    async getUserData() {
      const usuarioGitHub = 'ericajv';
      const urlPerfil = `https://api.github.com/users/${usuarioGitHub}`;

      const data = await fetch(urlPerfil)
      this.dadosGitHub = await data.json()
    }
  },
  components:{
    TheHeader
  }
};

</script>

<template>
  <TheHeader></TheHeader>
  <div>
    <button @click="getUserData">Seach</button>
    <pre>{{ dadosGitHub }}</pre>

  </div>
</template>

<style>
.container {
  background-color: green;
  border-radius: 5rem;
}
</style>
