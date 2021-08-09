<template>
  <div id="app">
    <!--<img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>-->
    <Pomodoro numberOfBlocks="4" minutesWork="25" minutesPause="5" minutesLongPause="30" />
  </div>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
import Pomodoro from './components/Pomodoro.vue' 

export default {
  name: 'App',
  components: {
    //HelloWorld,
    Pomodoro
  }
}
</script>

<style>
/*
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
*/
body{
  background-color: #2f3640/*#ee5253*/;
}
</style>
