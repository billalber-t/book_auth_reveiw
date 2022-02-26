<template>
    <v-app>
    <Nav />

    <v-main>
      <router-view />
    </v-main>
  </v-app>
  
</template>

<script>
// import HelloWorld from "../components/HelloWorld";
import Nav from "../components/Home/Nav.vue"

export default {
  name: "Home",

  components: {
    // HelloWorld,
    Nav,
  },
};
</script>
