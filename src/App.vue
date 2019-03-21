<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <VueRollUp 
    :rollList="rollList"
    />
  </div>
</template>

<script>
import VueRollUp from './components/VueRollUp'

export default {
  name: 'app',
  data () {
    return {
      rollList: [
        'A','B','C'
      ]
    }
  },
  components: {
    VueRollUp
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
