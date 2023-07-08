<template>
  <div class="Home">

<div class="container">
    <div class="input-group mb-3">
  <input type="text" class="form-control" placeholder="Search any Pokemon" aria-label="Recipient's username" aria-describedby="basic-addon2" id="searchbar">
        <span>
            <button class="btn btn-primary">
                Search
            </button>
        </span>
</div>
</div>      


    <div class="mt-3">
    <div class="row d-flex justify-contetn-around">
      <div class="col-sm-2 col" v-for="pokemon in pokemons" v-bind:key="pokemon">
        <div class="card" style="width: 18rem">
          <img :src="pokemon.image" class="card-img-top img-fluid" alt="..." />
          <div class="card-body">
            <h5 class="card-title fs-2">{{ pokemon.name }}</h5>
            <p class="card-text">Type: {{ pokemon.type }}</p>
          </div>
        </div>
      </div>
    </div>
   
  </div>
</div>
</template>

<script>
export default {
    
  name: "HomePage",
  data() {
    return {
      pokemons: [],
    };
  },
  mounted() {
    this.fetchPokemon();
    this.search_pokemon();
  },
  methods: {
    fetchPokemon() {
      const promises = [];
      for (let i = 1; i <= 20; i++) {
        const url = `https://pokeapi.co/api/v2/pokemon/${i}`;
        promises.push(fetch(url).then((res) => res.json()));
      }
      Promise.all(promises).then((results) => {
        this.pokemons = results.map((result) => ({
          name: result.name,
          image: result.sprites["front_default"],
          type: result.types.map((type) => type.type.name).join(", "),
          id: result.id,
        }));
      });
    },
    search_pokemon() { 
    let input = document.getElementById('searchbar').value 
    input=input.toLowerCase(); 
    let x = document.getElementsByClassName('card'); 
      
    for (let i = 0; i < x.length; i++) {  
        if (!x[i].innerHTML.toLowerCase().includes(input)) { 
            x[i].style.display="none"; 
        } 
        else { 
            x[i].style.display="list-item";                  
        } 
    } 
}
  }
};


</script>
