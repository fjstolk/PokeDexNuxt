<template>
<div>
    <h1>PokeDex</h1>
    <div id="poke_container" class="poke-container"></div>
<div>
</template>

<script>
const poke_container = document.getElementById("poke_container");
const pokemons_number = 150;

const fetchPokemons = async () => {
  for (let i = 1; i <= pokemons_number; i++) {
    await getPokemon(i);
  }
};

const getPokemon = async (id) => {
  const url = `https://pokeapi.co/api/v2/pokemon/${id}`;
  const res = await fetch(url);
  const pokemon = await res.json();
  createPokemonCard(pokemon);
};

const createPokemonCard = (pokemon) => {
  const pokemonEl = document.createElement("div");
  pokemonEl.classList.add("pokemon");
  const { id, name, sprites, types } = pokemon;
  const type = types[0].type.name;
  const pokeInnerHTML = `
  <div class="img-container">
    <img src="${sprites.front_default}" alt="${name}" />
  </div>
  <div class="info">
    <span class="number">${id}</span>
    <h3 class="name">${name}</h3>
    <small class="type">Type: <span>${type}</span></small>
  </div>
  `;
  pokemonEl.innerHTML = pokeInnerHTML;
  poke_container.appendChild(pokemonEl);
};

fetchPokemons();

</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Muli&display=swap');
@import url('https://fonts.googleapis.com/css?family=Lato:300,400&display=swap');

* {
	box-sizing: border-box;
}

body {
	background: #ffc600;
	background: linear-gradient(to right, #D4D3DD, #ff6600);
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
	font-family: 'Lato';
	margin: 0;
}

h1 {
	letter-spacing: 3px;
}

.poke-container {
	display: flex;
	flex-wrap: wrap;
	align-items: space-between;
	justify-content: center;
	margin: 0 auto;
	max-width: 1200px;
}

.pokemon {
	background-color: #eee;
	border-radius: 20px;
	box-shadow: 0 3px 15px rgba(100, 100, 100, 0.5);
	margin: 10px;
	padding: 20px;
	text-align: center;
}

.pokemon .img-container {
	background-color: rgba(255, 255, 255, 0.6);
	border-radius: 50%;
	width: 120px;
	height: 120px;
	text-align: center;
}

.pokemon .img-container img {
	margin-top: 20px;
	max-width: 90%;
}

.pokemon .info {
	margin-top: 20px;
}

.pokemon .number {
	background-color: rgba(0, 0, 0, 0.1);
	border-radius: 10px;
	font-size: 0.8em;
	padding: 5px 10px;
}

.pokemon .name {
	margin: 15px 0 7px;
	letter-spacing: 1px;
} 
</style>