<template>
  <div :class="{input: true, focused: isFocused}">
    <input
      class="input__search"
      @focus="isFocused = true"
      @blur="isFocused = false"
      placeholder="Поиск по ФИО"
      ref="input"
      @input="inputHandler"
    >
    <button class="input__button">
      <SearchIcon/>
    </button>
  </div>
</template>

<script>
import SearchIcon from '@/components/icons/SearchIcon.vue';

export default {
  name: 'TheInput',
  components: { SearchIcon },
  data() {
    return {
      isFocused: false,
    };
  },
  methods: {
    inputHandler() {
      this.$emit('input', this.$refs.input.value);
    },
  },
};
</script>

<style lang="scss" scoped>
.input {
  padding: 11px 12px;
  max-width: 304px;
  height: 40px;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  border: 1px solid var(--gray);
  border-radius: var(--input-rad);
  transition: var(--transition);

  &.focused {
    border-color: var(--red);

    svg {
      color: var(--red);
    }
  }

  &:hover {
    border-color: var(--red);

    svg {
      color: var(--red);
    }
  }

  .input__search {
    flex: 1 1 0;
  }

  .input__button {
    cursor: pointer;
    width: 16px;
    height: 16px;
    color: var(--blue);

    svg {
      transition: var(--transition);
    }
  }

  @media screen and (max-width: 768px) {
    max-width: 100%;
    width: 100%;
  }

  @media screen and (max-width: 428px) {

  }
}
</style>
