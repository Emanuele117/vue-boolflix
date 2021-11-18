<template>
  <div class="container">
    <input v-model="movieName" type="text" name="search" id="search" />
    <button @click="searchMovies">Search a Movie</button>

    <div v-for="movie in movies" :key="movie.id">
      <h2>{{ movie.title }}</h2>
      <h3>{{ movie.original_title }}</h3>
      <p>{{ movie.original_language }}</p>
      <p>{{ movie.vote_avarage }}</p>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      movieName: "",
      movies: [],
    };
  },
  methods: {
    searchMovies() {
      axios
        .get(
          "https://api.themoviedb.org/3/search/movie?api_key=2f8b947658c764e57b4f430bb9ca5991&language=en-US&query=movieName&page=1&include_adult=false"
        )
        .then((r) => {
          console.log(r.data);
          this.movies = r.data.movie;
        })
        .catch((e) => {
          console.log(e, "OPS");
        });
    },
  },
};
</script>

<style>
</style>