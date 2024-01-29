<script>
import TheHeader from './components/TheHeader.vue'
export default {
  data() {
    return {
      userData: {
        bio: "",
        name: "",
        login: "",
        followers: "",
        following: "",
        public_repos: "",
        id: "",

      },
      user: ""
    };
  },
  methods: {
    async getUserData() {
      const url = `https://api.github.com/users/${this.user}`;
      const data = await fetch(url)
      this.userData = await data.json()
    }
  },
  components: {
    TheHeader
  }
};

</script>

<template>
  <TheHeader></TheHeader>
  <div class="container">
    <div class="form">
      <input type="text" placeholder="GitHub User" id="User" v-model="user">
      <button @click="getUserData">Search</button>
      </div>


    <div class="infos" v-if="userData.name">
      <img :src="userData.avatar_url" :alt="userData.name" />
      <h2>{{ userData.bio }} </h2>
      <h3> Name: {{ userData.name }} </h3>
      <h3>Username: {{ userData.login }}</h3>
      <h3>Followers: {{ userData.followers }}</h3>
      <h3>Following: {{ userData.following }}</h3>
      <h3>Repositories count: {{ userData.public_repos }}</h3>
        </div>

  </div>
</template>

<style>
.form {
  background-color: green;
  border-radius: 5rem;

}
.container{
  background-color: yellow;
}
.infos{
  background-color: orange;
}
</style>
