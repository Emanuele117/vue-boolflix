<template>
  <div class="container movieAndSeries">
    <SiteHeader @search-tvshows="search" />
    <h1>Results for Movies:</h1>
    <div class="container movies">
      <div class="movie" v-for="movie in movies" :key="movie.id">
        <img
          :src="`https://image.tmdb.org/t/p/w200/${movie.poster_path}`"
          alt=""
        />
        <h2>{{ movie.title }}</h2>
        <h3>{{ movie.original_title }}</h3>
        <p>{{ movie.original_language }} | {{ movie.vote_average }}</p>
        <img
          :src="
            require(`../assets/img-bandiere/${movie.original_language}.png`)
          "
          alt=""
        />
        <hr />
      </div>
    </div>
    <h1>Results for Series:</h1>
    <div class="container series">
      <div class="serieTv" v-for="serie in series" :key="serie.id">
        <img
          :src="`https://image.tmdb.org/t/p/w200/${serie.poster_path}`"
          alt=""
        />
        <h2>{{ serie.name }}</h2>
        <h3>{{ serie.original_name }}</h3>
        <p>{{ serie.original_language }} | {{ serie.vote_average }}</p>
        <img
          :src="
            require(`../assets/img-bandiere/${serie.original_language}.png`)
          "
          alt=""
        />
        <hr />
      </div>
    </div>
  </div>
</template>

<script>
import SiteHeader from "./SiteHeader.vue";
import axios from "axios";

export default {
  data() {
    return {
      searchString: "",
      movies: [],
      series: [],
      movies_url: "https://api.themoviedb.org/3/search/movie",
      series_url: "https://api.themoviedb.org/3/search/tv",
      api_key: "2f8b947658c764e57b4f430bb9ca5991",
    };
  },
  methods: {
    search(searchString) {
      const full_url = `${this.movies_url}?api_key=${this.api_key}&query=${searchString}`;
      const series_url = `${this.series_url}?api_key=${this.api_key}&query=${searchString}`;

      axios
        .get(full_url)
        .then((r) => {
          console.log(r.data);
          this.movies = r.data.results;
        })
        .catch((e) => {
          console.log(e, "OPS");
        });

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
  components: {
    SiteHeader,
  },
};
</script>

<style lang="scss">
.movies {
  display: flex;
}
.series {
  display: flex;
}
</style>