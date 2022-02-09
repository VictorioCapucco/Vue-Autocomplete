<template>
  <div>
    {{ teste }}
    <img alt="Vue logo" src="./assets/logo.png" />
    <div class="teste">
      <autocomplete
        v-model="test"
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
        test: {},
        items: [
          { name: "Banana", id: 1, color: "Yellow" },
          { name: "Strawberry", id: 2, color: "Red" },
          { name: "Orange", id: 3, color: "Orange" },
          { name: "Lemon", id: 4, color: "Green" },
          { name: "Pineapple", id: 5, color: "Yellow" },
          { name: "Watermelon", id: 6, color: "Red" },
          { name: "Melon", id: 7, color: "Yellow" },
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
