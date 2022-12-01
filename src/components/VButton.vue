<template>
  <button
    class="button"
    :class="{
      blue: this.$props.color==='blue',
      red: color==='red',
      outline: outline,
      small: small,
    }"
  >
    <slot>Button</slot>
  </button>
</template>

<script>
export default {
  name: 'VButton',
  props: {
    outline: {
      type: Boolean,
      required: false,
    },
    color: {
      type: String,
      required: false,
    },
    small: {
      type: Boolean,
      required: false,
    },
  },
};
</script>

<style lang="scss" scoped>
.button {
  display: flex;
  align-items: center;
  justify-content: center;

  border: 0;
  font-weight: var(--m);
  line-height: var(--btn-lh);
  color: var(--white);
  width: 100%;
  min-width: var(--large-btn);
  max-width: var(--large-btn);
  height: 40px;
  border-radius: var(--btn-rad);

  cursor: pointer;

  transition: var(--transition);

  svg {
    margin-right: var(--icon-margin);
  }

  &.red {
    background-color: var(--red);

    &:hover {
      background-color: var(--red-darken);
    }
  }

  &.blue {
    background-color: var(--blue);

    &:hover {
      background-color: var(--blue-darken);
    }
  }

  &.outline {
    border: 1px solid var(--red);
    background-color: var(--white);
    color: var(--red);

    &:hover {
      background-color: var(--red-darken);
      color: var(--white);
      border-color: var(--red-darken);

      svg {
        fill: var(--white);
      }
    }
  }

  &.small {
    min-width: var(--small-btn);
    max-width: var(--small-btn);
  }
}
</style>
