<template>
  <div class="loader">
    <div class="bullet"></div>
    <div class="bullet"></div>
    <div class="bullet"></div>
  </div>
</template>

<script>
  export default {
    name: 'loader'
  }
</script>

<style scoped>
  .loader {
    display: flex;
    width: 50%;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    margin: 3em auto 0 auto;
  }

  .bullet {
    width: 1em;
    height: 1em;
    background: #ccc;
    border-radius: 50%;
    margin: 0 1em;
  }

  .bullet:nth-child(1) {
    animation: bounce .5s infinite ease-in-out;
  }
  .bullet:nth-child(2) {
    animation: bounce .5s .1s infinite ease-in-out;
  }
  .bullet:nth-child(3) {
    animation: bounce .5s .2s infinite ease-in-out;
  }

  @keyframes bounce {
    0% {
      transform: scale3d(1, 1, 1);
      opacity: 1;
    }
    50% {
      transform: scale3d(1.4, 1.4, 1.4);
      opacity: .1;
    }
    100% {
      transform: scale3d(1, 1, 1);
      opacity: 1;
    }
  }
</style>
