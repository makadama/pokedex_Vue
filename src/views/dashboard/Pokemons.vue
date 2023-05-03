<template>
    <div class="container">
      <div class="section">
        <div class="columns">
          <div class="column has-text-centered">
            <h1 class="title" style="color: ghostdark;">Pokemons</h1><br>
          </div>
          <hr>
        </div>
        <div class="columns">
            <form @submit.prevent="getPokemons">
                <div class="field has-addons">
                    <div class="control">
                        <input type="text" class="input" v-model="query">
                    </div>
                    <div class="control">
                        <button class="button is-success">Search</button>
                    </div>
                </div>
            </form>
        </div>
        <div id="app" class="row columns is-multiline">
          <div  v-for="pokemon in pokemons"  v-bind:key="pokemon.id" class="column is-4">
            <div class="card large">
              <div class="card-image has-text-centered">
                <figure class="image is-5by5 is-128x128 is-inline-block">
                  <img :src="`https://raw.githubusercontent.com/HybridShivam/Pokemon/master/assets/images/${pokemon.id}.png`" alt="Image">
                </figure>
              </div>
              <div class="card-content">
                <div class="media">
                  <div class="media-content  has-text-centered">
                    <p class="title is-4 no-padding">Name: {{pokemon.name}}</p>
                    <p>
                      <span class="title is-6">
                        Type: {{pokemon.type_1}}
                      </span>
                    </p>
                    <p class="subtitle is-6">Generation: {{pokemon.generation}}</p>
                  </div>
                </div>
                <div class="content">
                   <span class="title is-6">
                       <router-link :to="{ name: 'Pokemon', params: { id: pokemon.id }}">Details</router-link>
                    </span>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="buttons">
            <button class="button is-light" @click="goToPreviousPage()" v-if="showPreviousButton">Previous</button>
            <button class="button is-light" @click="goToNextPage()" v-if="showNextButton">Next</button>
        </div>
      </div>
    </div>
</template>

<script>
    import axios from 'axios'
    export default{
        name : 'Pokemons',
        data(){
            return {
                pokemons : [],
                showNextButton: false,
                showPreviousButton: false,
                currentPage : 1,
                query: '',
            }
            },
        mounted(){
            this.getPokemons()
        },
        methods: {
            goToNextPage() {
                this.currentPage += 1
                this.getPokemons()
            },
            goToPreviousPage() {
                this.currentPage -= 1
                this.getPokemons()
            },
            async getPokemons(){
            this.$store.commit('setIsLoading', true)
            this.showNextButton = false
            this.showPreviousButton = false

            await axios
            .get(`/api/v1/pokemons/?page=${this.currentPage}&search=${this.query}`)
            .then(response => {
            this.pokemons = response.data.results
            if (response.data.next) {
                this.showNextButton = true
            }
            if (response.data.previous) {
                this.showPreviousButton = true
            }
            })
            .catch(error => {
                console.log(error)
            })

            this.$store.commit('setIsLoading', false)
            
            }
        }
    }
</script>
