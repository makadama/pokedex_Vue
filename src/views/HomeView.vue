<template>
  <section class="hero is-primary is-bold">
    <div class="hero-body splash">
        <div class="container">
            <div class="columns is-vcentered">
                <div class="column">
                    <h1 class="title is-spaced is-size-2-desktop is-size-1-fullhd"> Bowo Test Assessment</h1>

                    <h2 class="subtitle">
                        App Built with Django and Sqlite on the back-end, VueJS and Bulma css on the Front-end
                    </h2>

                    <div class="buttons">
                        <router-link :to="{ name: 'Pokemons'}" class="control button is-primary is-inverted is-medium">See Pokemons →</router-link>
                    </div>
                </div>

                <div class="column">
                  <figure class="image is-16x9">
                    <img src="https://www.rappler.com/tachyon/2022/12/Pokemon-December-17-2022-003.jpg">
                  </figure>
                </div>
            </div>
        </div>
    </div>
</section>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'HomeView',
  components: {
    HelloWorld
  }
}
</script>
