<template lang="pug">
  .loading-spinner
</template>

<script>
export default {
  name: "LoadingSpinner"
};
</script>

<style lang="scss" scoped>
.loading-spinner {
  bottom: 2rem;
  display: inline-block;
  height: 20px;
  left: 1rem;
  position: absolute;
  width: 20px;

  &:after {
    animation: rotate 1.2s linear infinite;
    border: 4px solid #fff;
    border-color: #fff transparent #fff transparent;
    border-radius: 50%;
    content: " ";
    display: block;
    height: 100%;
    width: 100%;
  }
}

@keyframes rotate {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
