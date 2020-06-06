<template>
  <v-app>
    <router-view></router-view>
  </v-app>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  name: "App",

  components: {},

  data: () => ({
    //
  })
});
</script>

<style lang="scss">
#app {
  font-family: "Avenir";
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
