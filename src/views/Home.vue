<template>
  <div class="row bg">
    <div class="col-12">
      <Header />
    </div>
    <div class="col-12">
      <Content />
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Header from "@/components/Header.vue";
import Content from "@/components/Content.vue";

export default {
  name: "Home",
  components: {
    Header,
    Content
  }
};
</script>

<style lang="scss">
.bg {
  background: rgb(69, 94, 204) url("../assets/img/bg.png") no-repeat fixed
    bottom left;
}

#align-mid {
  display: flex;
  align-items: center;
}
</style>
