<template>
  <div>
    <img alt="Vue logo" src="./assets/logo.png" />
    <div class="teste">
      <autocomplete v-model="teste" :items="items" />
    </div>
  </div>
</template>

<script>
  import autocomplete from "./components/autocomplete.vue";

  export default {
    name: "App",
    components: {
      autocomplete,
    },
    data() {
      return {
        teste: "",
        items: [
          "Banana",
          "Morango",
          "Caju",
          "Laranja",
          "Limão",
          "Abacaxi",
          "Manga",
          "Melancia",
          "Melão",
        ],
      };
    },
  };
</script>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
  .teste {
    background-color: gray;
    width: 50%;
    height: 500px;
    padding: 20px;
    margin-left: auto;
    margin-right: auto;
  }
</style>
