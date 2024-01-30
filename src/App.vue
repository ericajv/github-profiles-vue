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
                repos: []
            },
            user: ""
        };
    },
    methods: {
        async getUserData() {
            const userUrl = `https://api.github.com/users/${this.user}`;
            const reposUrl = `https://api.github.com/users/${this.user}/repos?sort=created&per_page=4`;
            this.userData = await this.fetchData(userUrl)
            this.userData.repos = await this.fetchData(reposUrl)
        },
        async fetchData(url) {
            const data = await fetch(url)
            return await data.json()
        }
    },
    components: { TheHeader }
};
</script>

<template>
    <TheHeader />
    <div class="container">
        <div class="form">
            <input type="text" placeholder="GitHub User" id="User" v-model="user" v-on:keyup.enter="getUserData">
            <button @click="getUserData">Search</button>
        </div>

        <div class="bio" v-if="userData.name">
            <img :src="userData.avatar_url" :alt="userData.name" />
            <h2>{{ userData.bio }} </h2>
        </div>

        <div class="infos" v-if="userData.name">
            <div class="details">
                <h3>Name: {{ userData.name }} </h3>
                <h3>Username: {{ userData.login }}</h3>
                <h3>Followers: {{ userData.followers }}</h3>
                <h3>Following: {{ userData.following }}</h3>
                <h3>Repositories count: {{ userData.public_repos }}</h3>
            </div>
            <div class="repos">
                <a v-for="repo in userData.repos" :key="repo.id" :href="repo.html_url" target="_blank">
                    {{ repo.name }}
                    <br>
                </a>
            </div>
        </div>
    </div>
</template>

<style>
.form {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 1rem;

    >input {
        color: #140f0b;
        padding: 1rem;
        background-color: #a49df9;
        width: 20rem;
        height: 3rem;
        border: none;
        border-radius: 5px 0 0 5px;
        font-size: 1rem;
        font-weight: bold;
        outline: none;
    }

    ::placeholder {
        color: #5563ac;
        font-size: 1rem;
        border: none;
    }
}

.bio {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    text-align: center;
    padding: 1rem;
    color: #95a0fa;
    font-size: 1.2rem;

    >img {
        height: 15rem;
        border-radius: 50%;
        margin-bottom: 1rem;
    }
}

.infos {
    display: flex;
    justify-content: center;
    gap: 5rem;
    font-weight: lighter;
    font-family: inherit;
    color: #4f60a5;
    padding: 2rem 5rem;
    line-height: 2rem;
    font-size: 1.5rem;
}

.repos {
    >a {
        color: #4f60a5;
        text-decoration: none;
        line-height: .5rem;
        font-weight: bold;
        font-size: 1.2rem;
    }

    a:hover {
        color: #95a0fa;
        text-decoration: underline #95a0fa;
    }
}
</style>
