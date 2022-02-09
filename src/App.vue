<template>
  <div>
    {{ teste }}
    <img alt="Vue logo" src="./assets/logo.png" />
    <div class="teste">
      <autocomplete
        v-model="teste"
        :items="items"
        displayed="name"
        :returned="['id', 'name']"
      />
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
        teste: {},
        items: [
          { name: "Banana", id: 1, teste: "teste" },
          { name: "Morango", id: 2, teste: "teste" },
          { name: "Caju", id: 3, teste: "teste" },
          { name: "Laranja", id: 4, teste: "teste" },
          { name: "Limão", id: 5, teste: "teste" },
          { name: "Abacaxi", id: 6, teste: "teste" },
          { name: "Manga", id: 7, teste: "teste" },
          { name: "Melancia", id: 8, teste: "teste" },
          { name: "Melão", id: 9, teste: "teste" },
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
