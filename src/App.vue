<template>
  <div id="app">
    <Pomodoro numberOfBlocks="4" minutesWork="25" minutesPause="5" minutesLongPause="30" />
  </div>
</template>

<script>
import Pomodoro from './components/Pomodoro.vue' 

export default {
  name: 'App',
  components: {
    Pomodoro
  }
}
</script>

<style>
body{
  background-color: #2f3640;
}
</style>
