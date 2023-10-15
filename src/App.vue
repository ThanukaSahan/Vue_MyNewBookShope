<template>
  <NavigationBar />
  <router-view />
</template>

<script>
// @ is an alias to /src
import NavigationBar from "@/components/NavigationBar.vue";
import { library } from "@fortawesome/fontawesome-svg-core";
import { fas } from "@fortawesome/free-solid-svg-icons";
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";

library.add(fas);

export default {
  name: "HomeView",
  components: {
    NavigationBar,
    FontAwesomeIcon,
  },
};
</script>

<style>
</style>
