<template>
    <div>
        <nuxt-link to="/jokes">Back To Jokes</nuxt-link>
        <h2 class="joke">{{ joke }}</h2>
        <hr>
        <small>Joke ID: {{ $route.params.id }}</small>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    data() {
        return {
            joke: {}
        }
    },
    async created() {
        // send headers (requirements) through Axios
        const config = {
            headers: {
                'Accept': 'application/json'
            }
        }

        try {
            const res = await axios.get(`https://icanhazdadjoke.com/j/${this.$route.params.id}`, config);
            // console.log(res.data);
            this.joke = res.data.joke;
        } 
        catch(err) {
            console.log(err);
        }   
        
    },
    head() {
        return {
            title: this.joke,
            meta: [
                {
                    hid: 'description',
                    name: 'description',
                    content: 'Best place for corny dad jokes'
                }
            ]
        }
    }
}
</script>

<style>
    .joke {
        margin: 1rem 0 2rem;
    }
</style>