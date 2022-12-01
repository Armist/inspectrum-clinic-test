<template>
  <label for="checkbox">
    <input
      class="checkbox"
      id="checkbox"
      type="checkbox"
      v-model="checked"
      :value="item"
      @change="changeHandler"
    >
  </label>
</template>

<script>
export default {
  name: 'VCheckbox',
  props: ['value', 'item'],
  data() {
    return {
      checkValue: [],
    };
  },
  computed: {
    checked: {
      get() {
        return this.value;
      },
      set(val) {
        if (val.isArray) {
          val.forEach((item) => {
            this.checkValue.push(item);
          });
        } else {
          this.checkValue = val;
        }
      },
    },
  },
  methods: {
    changeHandler() {
      this.$emit('input', this.checkValue);
    },
  },
};
</script>

<style lang="scss" scoped>
label {
  display: block;
  width: 16px;
  height: 16px;
}

.checkbox {
  width: 16px;
  height: 16px;
  appearance: none;
  margin: 0;
  font: inherit;
  color: var(--red);
  border: 1px solid var(--red);
  border-radius: var(--checkbox-rad);
  transform: translateY(-0.075em);
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;

  &::before {
    border-radius: 1px;
    content: "";
    padding: 5px;
    transform: scale(0);
    transition: all .1s ease-in-out;
    box-shadow: inset 1em 1em var(--red);
  }

  &:checked {
    &:before {
      transform: scale(1);
    }
  }
}
</style>
