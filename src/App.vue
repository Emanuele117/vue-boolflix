<template>
  <div id="app">
    <SiteMain />
  </div>
</template>

<script>
import SiteMain from "./components/SiteMain.vue";
export default {
  name: "App",
  components: {
    SiteMain,
  },
};
</script>

<style lang="scss">
@import "../node_modules/bootstrap/scss/bootstrap.scss";
</style>
