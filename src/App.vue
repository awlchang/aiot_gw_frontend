<template>
  <v-app v-cloak>
    <v-main>
      <router-view></router-view>
    </v-main>
  </v-app>
</template>

<style>
[v-cloak] {
  display: none;
}
</style>

<script>
// import Login from "./components/Login";

export default {
  name: "App",

  // components: {
  //   // Login
  // },

  data: () => ({
    //
  })
};
</script>
