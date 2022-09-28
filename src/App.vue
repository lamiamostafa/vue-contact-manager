<template>
  <!-- <Spinner></Spinner> -->
  <NavBar></NavBar>
  <router-view></router-view>
</template>

<script>
import NavBar from "@/components/NavBar.vue";
// import NavBar from "@/components/NavBar.vue";

export default {
  name: 'App',
  components: { NavBar }
}
</script>

<style>

</style>
