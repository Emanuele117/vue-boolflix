<template>
  <header>
    <input
      v-model="searchString"
      type="text"
      name="search"
      id="search"
      placeholder="Search a Movie"
    />
    <button @click="$emit('search-tvshows', searchString)">Search</button>
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

<style>
</style>