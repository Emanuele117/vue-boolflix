<template>
  <div class="container movieAndSeries">
    <div class="movies">
      <input
        v-model="searchString"
        type="text"
        name="search"
        id="search"
        placeholder="Search a Movie"
      />
      <button @click="search">Search</button>

      <div class="movie" v-for="movie in movies" :key="movie.id">
        <h2>{{ movie.title }}</h2>
        <h3>{{ movie.original_title }}</h3>
        <p>{{ movie.original_language }} | {{ movie.vote_average }}</p>
        <hr />
      </div>
    </div>
    <div class="series">
      <input type="text" placeholder="Search Series" v-model="seriesString" />
      <button @click="searchSeries">Search</button>

      <div class="serieTv" v-for="serie in series" :key="serie.id">
        <h2>{{ serie.name }}</h2>
        <h3>{{ serie.original_name }}</h3>
        <p>{{ serie.original_language }} | {{ serie.vote_average }}</p>
        <hr />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      searchString: "",
      seriesString: "",
      movies: [],
      series: [],
      movies_url: "https://api.themoviedb.org/3/search/movie",
      series_url: "https://api.themoviedb.org/3/search/tv",
      api_key: "2f8b947658c764e57b4f430bb9ca5991",
    };
  },
  methods: {
    search() {
      const full_url = `${this.movies_url}?api_key=${this.api_key}&query=${this.searchString}`;

      axios
        .get(full_url)
        .then((r) => {
          console.log(r.data);
          this.movies = r.data.results;
        })
        .catch((e) => {
          console.log(e, "OPS");
        });
    },
    searchSeries() {
      const series_url = `${this.series_url}?api_key=${this.api_key}&query=${this.seriesString}`;

      axios
        .get(series_url)
        .then((r) => {
          console.log(r.data);
          this.series = r.data.results;
        })
        .catch((e) => {
          console.log(e, "OPS");
        });
    },
  },
};
</script>

<style lang="scss">
.movieAndSeries {
  display: flex;
  justify-content: space-around;
}
</style>