# vue-autocomplete

## Vue autocomplete
```
npm install vue-autocomplete-input-tag
```

## Usage
```html
<template>
  <div>
     <autocomplete v-model="teste" :items="items" />
  </div>
</template>

<script>
  import autocomplete from 'vue-autocomplete-input-tag'

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
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
