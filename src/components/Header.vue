<template>
  <div class="container">
    <div class="row" id="align-mid">
      <div class="col-6 text-left">
        <img :src="require('../assets/img/test.png')" alt="test" />
      </div>
      <div class="col-6 text-right">
        <img :src="require('../assets/img/fe.png')" alt="fe" />
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
export default Vue.extend({
  name: "Header"
});
</script>

<style></style>
