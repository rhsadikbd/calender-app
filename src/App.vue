<template>
  <calender-app />
</template>

<script>
import Calender from './components/Calender.vue'

export default {
  name: 'App',
  components: {
    'calender-app': Calender
  }
}
</script>

<style>
body{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    background-color: #00bac4;
    height: 100vh;
    font-family: sans-serif;
}
</style>
