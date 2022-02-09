<template>
  <div>
    <input
      class="autocomplete-input"
      :class="error ? 'autocomplete-error' : ''"
      :style="`height: ${inputHeight}px;`"
      v-model="typed"
      :disabled="isLoading && disableWhenLoading"
      @input="
        !openItems ? (openItems = true) : '',
          updateInput($event.target.value, false)
      "
      @focus="openItems = true"
      @blur="closeItems"
    />
    <div
      class="autocomplete-items"
      :style="`display: ${openItems ? 'grid' : 'none'};`"
    >
      <!-- Use @mousedown because @click occurs after @blur and make bugs -->
      <div
        v-for="item in filteredItems"
        :key="item"
        @mousedown="updateInput(item, true)"
        class="autocomplete-item"
      >
        {{ displayed != null ? item[displayed] : item }}
      </div>
    </div>
  </div>
</template>
<script>
  export default {
    data() {
      return {
        openItems: false,
        typed: "",
      };
    },
    computed: {
      filteredItems() {
        if (this.displayed !== null)
          return this.items.filter((item) => {
            return item[this.displayed]
              .toString()
              .toLowerCase()
              .includes(this.typed.toLowerCase());
          });
        else
          return this.items.filter((item) => {
            return item
              .toString()
              .toLowerCase()
              .includes(this.typed.toLowerCase());
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
      permitArbitraryValues: {
        type: Boolean,
        default: false,
      },
      modelValue: {},
      error: {
        type: Boolean,
        default: false,
      },
      inputHeight: {
        type: Number,
        default: 30,
      },
      isLoading: {
        type: Boolean,
        default: false,
      },
      displayed: {
        type: String,
        default: null,
      },
      returned: {
        default: null,
      },
    },
    methods: {
      closeItems() {
        this.openItems = false;

        if (
          !this.permitArbitraryValues &&
          this.displayed === null &&
          this.returned === null
        ) {
          if (
            this.items.find((element) => this.modelValue === element) ===
            undefined
          )
            this.updateInput("", false);
        }
      },
      updateInput(value, clicked) {
        if (this.displayed !== null) {
          if (clicked) {
            this.typed = value[this.displayed];
            if (this.returned === null) this.$emit("update:modelValue", value);
            else if (typeof this.returned === "string")
              this.$emit("update:modelValue", value[this.returned]);
            else {
              let objectValue = {};
              for (let i = 0; i < this.returned.length; i++) {
                objectValue[this.returned[i]] = value[this.returned[i]];
              }
              this.$emit("update:modelValue", objectValue);
            }
          } else this.$emit("update:modelValue", { typed: this.typed });
        } else {
          this.$emit("update:modelValue", value);
          this.typed = value;
        }
      },
    },
  };
</script>
<style>
  .autocomplete-input {
    width: 100%;
    border: 1px solid transparent;
    color: #666;
    border-radius: 10px;
    outline: none;
    padding: 9px 14px;
    box-sizing: border-box;
    font-size: 14px;
  }
  .autocomplete-items {
    max-height: 200px;
    margin-top: 8px;
    width: 100%;
    background-color: white;
    border-radius: 8px;
    overflow: auto;
  }
  .autocomplete-item {
    padding: 6px 16px;
    color: #4a4a4a;
    max-width: 100%;
    cursor: pointer;
    text-align: left;
    font-size: 14px;
  }
  .autocomplete-error {
    border: 1px solid red;
  }
  .autocomplete-item:hover {
    background-color: #e8e8e8;
  }
</style>
