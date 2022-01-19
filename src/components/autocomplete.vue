<template>
  <div>
    <input
      class="input"
      :class="error ? 'error' : ''"
      :style="`height: ${inputHeight}px;`"
      :value="modelValue"
      :disabled="isLoading && disableWhenLoading"
      @input="
        !openItems ? (openItems = true) : '', updateInput($event.target.value)
      "
      @focus="openItems = true"
      @blur="closeItems"
    />
    <div class="items" :style="`display: ${openItems ? 'grid' : 'none'};`">
      <!-- Use @mousedown because @click occurs after @blur and make bugs -->
      <div
        v-for="item in filteredItems"
        :key="item"
        @mousedown="updateInput(item)"
        class="item"
      >
        {{ item }}
      </div>
    </div>
  </div>
</template>
<script>
  export default {
    data() {
      return {
        openItems: false,
      };
    },
    computed: {
      filteredItems() {
        return this.items.filter((item) => {
          return item
            .toString()
            .toLowerCase()
            .includes(this.modelValue.toLowerCase());
        });
      },
    },
    props: {
      items: {
        type: Array,
        default: () => {
          return [];
        },
      },
      disableWhenLoading: {
        type: Boolean,
        default: false,
      },
      permitArbitratyValues: {
        type: Boolean,
        default: true,
      },
      modelValue: {
        type: String,
        default: "",
      },
      error: {
        type: Boolean,
        default: false,
      },
      inputHeight: {
        type: Number,
        default: 30,
      },
    },
    methods: {
      closeItems() {
        this.openItems = false;

        if (!this.permitArbitratyValues) {
          if (
            this.items.find((element) => this.modelValue === element) ===
            undefined
          )
            this.updateInput("");
        }
      },
      updateInput(value) {
        this.$emit("update:modelValue", value);
      },
    },
  };
</script>
<style scoped>
  .input {
    width: 100%;
    border: 1px solid transparent;
    color: #666;
    border-radius: 10px;
    outline: none;
    padding: 9px 14px;
    box-sizing: border-box;
    font-size: 14px;
  }
  .items {
    max-height: 200px;
    margin-top: 8px;
    width: 100%;
    background-color: white;
    border-radius: 8px;
    overflow: auto;
  }
  .item {
    padding: 6px 16px;
    color: #4a4a4a;
    max-width: 100%;
    cursor: pointer;
    text-align: left;
    font-size: 14px;
  }
  .error {
    border: 1px solid red;
  }
  .item:hover {
    background-color: #e8e8e8;
  }
</style>
