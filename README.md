# [![npm](https://img.shields.io/npm/dt/vue-autocomplete-input-tag.svg)]() [![npm](https://img.shields.io/npm/v/vue-autocomplete-input-tag.svg)]() [![npm](https://img.shields.io/npm/l/vue-autocomplete-input-tag.svg)]()

## Vue autocomplete
```
npm install vue-autocomplete-input-tag
```

## Usage
```html
<template>
  <div>
     <autocomplete v-model="test" :items="items" />
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
        test: "",
        items: [
          "Banana",
          "Strawberry",
          "Orange",
          "Lemon",
          "Pineapple",
          "Watermelon",
          "Melon",
        ],
      };
    },
  };
</script>
```

## Props
```html
<template>
  <div>
     <autocomplete 
        v-model="test" 
        :items="items" 
        isLoading="true" 
        :disableWhenLoading="true" 
        :permitArbitraryValues="true" 
        :error="true"
        :inputHeight="40" 
        displayed="name"
        :returned="['id', 'name']" 
     />
  </div>
</template>
<script>
  import autocomplete from 'vue-autocomplete-input-tag'
  
  export default {
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
      }
     }
</script>
```
<ul>
<li><h4>isLoading:</h4> You can inform the component if something is loading. It works with 'disableWhenLoading' prop. It's a Boolean prop, and the default value is false.</li>

<li><h4>disableWhenLoading:</h4> Disable input to user when the prop 'isLoading' is true. It's a Boolean prop, and the default value is false.</li>

<li><h4>permitArbitraryValues:</h4> If the user does not select some option and the input lose focus, this prop permit the digited value. It's a Boolean prop, and the default value is false.</li>

<li><h4>error:</h4> You can change the input's border color to red, when some error occurs. It's a Boolean prop, and the default value is false.</li>

<li><h4>inputHeight:</h4> With this prop you can modify the input's height, in px. It's a Number prop, and the default value is 30. </li>
  
<li><h4>displayed:</h4> With this prop you can pass an array of objects in "items" prop, and inform the displayed field. It's a String prop, and the default value is null. If you pass an array of objects and don't inform this prop, the autocomplete will not work correctly. </li>
  
<li><h4>returned:</h4> With this prop you can inform the returned value, when use an array of objects. You can inform a single string (It will return just this field), an array of strings (with the fields you want to return) or nothing (It will return all the properties from the object). Only inform this prop if items prop is an array of objects. </li>
</ul>

### How does the reactivity works?
If you pass an array of strings (first example) the return will be just a string with the typed value, and when you select some option will be the selected value. 

If you pass an array of objects (second example), when you type, the returned value will be an object with "typed" property. And when you select some option, will return what you inform in "returned" prop. The typed property is returned because you can use @input and refresh the array.

### References
"Como criar e publicar uma biblioteca (em Vue) no npm?" -> https://medium.com/tableless/como-criar-e-publicar-uma-biblioteca-em-vue-no-npm-2dff8271ca7d
