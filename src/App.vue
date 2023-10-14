<template>
  <NavigationBar />

  <router-view />
</template>

<script>
// @ is an alias to /src
import NavigationBar from "@/components/NavigationBar.vue";
export default {
  name: "HomeView",
  components: {
    NavigationBar,
  },
};
</script>

<style>
</style>
