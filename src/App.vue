<template>
  <div id="app">
    <div class="hero is-white is-gradient is-bold">
      <div class="hero-body">
        <h1 class="title">
          <span class="has-text-success">R&M</span>
          <span class="subtitle">Personajes</span>
        </h1>
        <button class="button is-success is-rounded" v-on:click="fetch">Consultar</button>
      </div>
    </div>

    <div class="container">
      <div class="columns is-desktop is-mobile is-tablet is-multiline is-centered">
        <character
          v-for="character of characters"
          v-bind:key="character.id"
          v-bind:character="character"
        />
      </div>
    </div>

    <nav class="pagination" role="navegation" aria-label="pagination">
      <a class="pagination-previous">Anterior</a>
      <ul class="pagination-list">
        <li>
          <a class="pagination-link is-current">{{ page }}</a>
        </li>
      </ul>
      <a class="pagination-next">Siguiente</a>
    </nav>
  </div>
</template>

<script>
//librerias
import axios from "axios";

import Character from "./components/Character";

export default {
  name: "App",
  components: {
    Character //character
  },
  data: function() {
    return {
      characters: [],
      page: 1,
      pages: 1
    };
  },
  created() {
    this.fetch();
  },
  methods: {
    fetch() {
      let result = axios
        .get("https://rickandmortyapi.com/api/character")
        .then(res => {
          this.characters = res.data.results;
          this.pages = res.data.info.pages;
          console.log(res.data);
        })
        .catch(err => {
          console.log(err);
        });
    }
  }
};
</script>

<style>
</style>
