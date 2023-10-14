<template>
  <NavBar />
  <div style="padding: 20px 30px;">
    <RouterView />
  </div>
</template>

<script>
import { RouterView } from "vue-router";
import Planner from './components/Planning.vue'
import NavBar from './views/Navbar.vue'

export default {
  name: "App",
  components: {
    RouterView,
    Planner,
    NavBar,
},
};
</script>