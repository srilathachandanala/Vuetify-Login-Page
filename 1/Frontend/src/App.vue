<template>
  <v-app class="app">
    <v-main>
     <router-view></router-view>

    </v-main>
  </v-app>
</template>

<script>



export default {
  name: 'App',

  components: {
 
  },

  data: () => ({
    //
  }),
}
</script>

<style>

.app {
 background-image: url('./assets/trees.png');
}

</style>

