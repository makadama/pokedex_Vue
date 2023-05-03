<template>
    <div class="container">
                <div class="columns is-vcentered">
                    <div class="column is-5 is-offset-1 landing-caption">
                        <h1 class="title is-1 is-bold is-spaced">
                            <a href="`https://raw.githubusercontent.com/HybridShivam/Pokemon/master/assets/images/${pokemon.id}.png`">{{pokemon.name}}</a> {{pokemon.type_1}}
                        </h1>
                        <h2 class="subtitle is-5 is-muted">
                            generation: {{pokemon.generation}}
                        </h2>
                        <h2 class="subtitle is-5 is-muted">
                            HP: {{pokemon.hp}}
                        </h2>
                        <h2 class="subtitle is-5 is-muted">
                            Attack: {{pokemon.attack}}
                        </h2>
                        <h2 class="subtitle is-5 is-muted">
                            Defense: {{pokemon.defense}}
                        </h2>
                        <h2 class="subtitle is-5 is-muted">
                            Legendary: {{pokemon.legendary}}
                        </h2>
                    </div>
                    <div class="column is-5">
                        <figure class="image is-4by4">
                            <img :src="`https://raw.githubusercontent.com/HybridShivam/Pokemon/master/assets/images/${pokemon.id}.png`"  alt="Bulma CSS - Fresh, open-source starter top image.">
                        </figure>
                    </div>
    
                </div>
            </div>
</template>
<script>
    import axios from 'axios'
    export default {
        name: 'Pokemon',
        data() {
            return {
                pokemon: {}
            }
        },
        mounted() {
            this.getPokemon()
        },
        methods: {
            async getPokemon() {
                this.$store.commit('setIsLoading', true)
                const pokemonID = this.$route.params.id
                await axios
                    .get(`/api/v1/pokemons/${pokemonID}/`)
                    .then(response => {
                        this.pokemon = response.data
                    })
                    .catch(error => {
                        console.log(error)
                    })
                this.$store.commit('setIsLoading', false)
            },
        }
    }
</script>