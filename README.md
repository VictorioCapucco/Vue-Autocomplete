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

### Props
```html
<template>
  <div>
     <autocomplete v-model="teste" :items="items" isLoading="true" :disableWhenLoading="true" :permitArbitratyValues="true" :error="true" :inputHeight="40" />
  </div>
</template>
```
<ul>
<li><h3>isLoading:</h3> You can inform the component if something is loading. It works with 'disableWhenLoading' prop. It's a Boolean prop, and the default value is false.</li>

<li><h3>disableWhenLoading:</h3> Disable input to user when the prop 'isLoading' is true. It's a Boolean prop, and the default value is false.</li>

<li><h3>permitArbitraryValues:</h3> If the user does not select some option and the input lose focus, this prop permit the digited value. It's a Boolean prop, and the default value is false.</li>

<li><h3>error:</h3> You can change the input's border color to red, when some error occurs. It's a Boolean prop, and the default value is false.</li>

<li><h3>inputHeight:</h3> With this prop you can modify the input's height, in px. It's a Number prop, and the default value is 30. </li>
</ul>

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
