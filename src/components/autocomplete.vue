<template>
  <div>
    <input
      v-model="typed"
      v-bind="$attrs"
      @input="
        !openItems ? (openItems = true) : '',
          updateInput($event.target.value, false)
      "
      @focus="openItems = true"
      @blur="closeItems"
    />
    <div
      class="vue-autocomplete-input-tag-items"
      :style="`display: ${openItems ? 'grid' : 'none'};`"
    >
      <!-- Use @mousedown because @click occurs after @blur and make bugs -->
      <div
        v-for="item in filteredItems"
        :key="item"
        @mousedown="updateInput(item, true)"
        class="vue-autocomplete-input-tag-item"
      >
        {{ displayed != null ? item[displayed] : item }}
      </div>
    </div>
  </div>
</template>
<script>
  export default {
    inheritAttrs: false,
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
