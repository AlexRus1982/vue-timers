<template>
  <div ref="timer_container" class="timer-wrapper">
    <Timers/>
  </div>
</template>

<script>
  //import Timer from './components/Timer.vue'
  import Timers from './components/Timers.vue'

  window.Timers = [];

  export default {
    name: 'App',
    components: {
      Timers,
    }
  }

</script>

<style>
  body {
    background: #353638;
    padding: 0px;
    margin: 0px;
  }

  .timer-wrapper {
    display: flex;
    flex-wrap: wrap;
    row-gap: 45px;
    column-gap: 50px;
    padding: 72px 53px;
    justify-content: flex-start;
  }

  @media (min-width: 880px) {
    .timer-wrapper {
      max-width: 775px;
    }

  }

  @media (min-width: 605px) and (max-width: 879px) {
    .timer-wrapper {
      max-width: 500px;
    }
  }

  @media (max-width: 604px) {
    .timer-wrapper {
      max-width: 225px;
    }
  }

  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    display: flex;
    justify-content: center;
  }
</style>
