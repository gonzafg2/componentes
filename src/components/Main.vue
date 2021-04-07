<template>
  <main>
    <h1>Pokemones</h1>
    <button @click="getData()" class="btn btn-primary my-4">
      Llamar a la PokeAPI
    </button>
    <div class="container mt-4" v-if="pokemones.length > 0">
      <div class="row">
        <div class="col-3 mb-4" v-for="(pokemon, i) in pokemones" :key="i">
          <div class="card">
            <img v-if="imgPoke" width="96" height="96" :src="imgPoke(i+1)" class="card-img-top mx-auto" alt="pokemon" />
            <div class="card-body">
              <h5 class="card-title text-capitalize">{{ pokemon.name }}</h5>
              <p class="card-text d-none">
                Some quick example text to build on the card title and make up
                the bulk of the card's content.
              </p>
              <a href="#" class="btn btn-success d-none">Go somewhere</a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  name: "Main",
  data() {
    return {
      pokemones: [],
    };
  },
  methods: {
    async getData() {
      const url = "https://pokeapi.co/api/v2/pokemon";
      try {
        const req = await fetch(url);
        const reqJSON = await req.json();
        // console.log(reqJSON.results);
        this.pokemones = reqJSON.results;
      } catch (error) {
        console.log(error);
      }
    },
    async imgPoke(id) {
      const url = "https://pokeapi.co/api/v2/pokemon/";
      const req = await fetch(url+id);
      const reqJSON = await req.json();
      console.log(reqJSON);
      return reqJSON.sprites.front_default;
    }
  },
};
</script>

<style scoped>
h1 {
  color: blue;
}
</style>
