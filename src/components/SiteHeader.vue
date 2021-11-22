<template>
  <header>
    <div>
      <img src="../assets/img-bandiere/logo.netflix.png" alt="" />
      <input
        v-model="searchString"
        type="text"
        name="search"
        id="search"
        placeholder="Search a Movie"
      />
      <button @click="$emit('search-tvshows', searchString)">Search</button>
    </div>
  </header>
</template>

<script>
export default {
  data() {
    return {
      searchString: "",
    };
  },
};
</script>

<style lang="scss">
header {
  height: 100px;
  background-color: black;
  img {
    height: 120px;
    margin-left: 1rem;
  }
  input {
    margin-left: 50rem;
  }
}
</style>