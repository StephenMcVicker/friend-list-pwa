<template lang="pug">
  .hamburger(@click="$emit('toggle-menu');")
    div(:data-open="menuIsOpen")
    div(:data-open="menuIsOpen")
    div(:data-open="menuIsOpen")
</template>

<script>
export default {
  props: {
    menuIsOpen: {
      default: false,
      type: Boolean,
      required: false
    }
  }
};
</script>

<style lang="scss" scoped>
.hamburger {
  position: fixed;
  bottom: 1rem;
  right: 1rem;

  display: flex;
  flex-flow: column nowrap;
  height: 2rem;
  justify-content: space-around;
  transition: all 0.2s;
  width: 2rem;

  [data-open="true"] {
    &:nth-child(1) {
      transform: rotate(45deg);
    }

    &:nth-child(2) {
      opacity: 0;
    }

    &:nth-child(3) {
      transform: rotate(-45deg);
    }
  }

  div {
    background-color: white;
    border-radius: 50vh;
    height: 0.25rem;

    /* animation */
    transform-origin: 1px;
    transition: all 0.2s;
    width: 2rem;
  }
}
</style>
