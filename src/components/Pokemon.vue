<template>
  <div>
    <h1>Pokemon API</h1>
    <section>
      <div class="bloc">
        <h2>Liste des 20 premiers Pokemons de l'API</h2>
        <table class="tableCss">
          <tr>
            <th>Identifiant</th>
            <th>Nom du Pokemon</th>
          </tr>
          <tr :key="index" v-for="(pokemon, index) in pokemons">
            <td>{{ index + 1 }}</td>
            <td>{{ pokemon.name }}</td>
          </tr>
        </table>
      </div>
      <div class="bloc">
        <h2>Détails d'un Pokemon</h2>
        <p>
          Sélectionner l'identifiant du Pokemon :
          <input type="number" id="pokeId" placeholder="Pokemon ID" min="1" />
          <button v-on:click="showPoke">Rechercher</button>
        </p>

        <div v-if="this.pokeDetails">
          <div>
            <p>Nom : {{ this.pokeDetails.name }}</p>
          </div>
          <div>
            <p>Taille : {{ this.pokeDetails.height }} pouce</p>
          </div>
          <div>
            <p>Poids : {{ this.pokeDetails.weight }} lbs</p>
          </div>
          <div>
            <p>Expériences : {{ this.pokeDetails.base_experience }}</p>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Pokemon",
  data() {
    return {
      pokemons: null,
      pokeDetails: null,
      pokeId: null,
    };
  },
  mounted() {
    axios
      .get("https://pokeapi.co/api/v2/pokemon/")
      .then((response) => (this.pokemons = response.data.results))
      .catch((error) => console.log(error));
  },
  methods: {
    showPoke: function () {
      axios
        .get(
          "https://pokeapi.co/api/v2/pokemon/" +
            document.getElementById("pokeId").value
        )
        .then((response) => (this.pokeDetails = response.data))
        .catch((error) => console.log(error));
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.bloc {
  float: left;
  width: 50%;
}

.tableCss {
  border: solid 1px #e6e5e5;
  margin: 0 auto;
}
.tableCss th {
  background-color: #0094ff;
  color: #fff;
  padding: 10px;
  text-align: center;
}
.tableCss td {
  border: solid 1px #e6e5e5;
  padding: 10px;
}
</style>
