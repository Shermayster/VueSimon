<template>
  <div id="app">
    <header>
      <span>Vue.js PWA</span>
    </header>
    <div class="center">
      <div class="flex">
        <btn :btnColor="red"></btn>
        <btn :btnColor="blue"></btn>
      </div>
      <div class="flex">
        <btn :btnColor="orange"></btn>
        <btn :btnColor="green"></btn>
      </div>
    </div>
    </div>
</template>

<script>
import Hello from './components/Hello'
import Btn from './components/Button'

export default {
  name: 'app',
  components: {
    Hello,
    Btn
  },
  data () {
    return {
      red: '#cb4e4e',
      blue: '#0e83cd',
      orange: '#fcad26',
      green: '#17954c'
    }
  }
}
</script>

<style>
body {
  margin: 0;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

main {
  text-align: center;
  margin-top: 40px;
}

header {
  margin: 0;
  height: 56px;
  padding: 0 16px 0 24px;
  background-color: #35495E;
  color: #ffffff;
}

header span {
  display: block;
  position: relative;
  font-size: 20px;
  line-height: 1;
  letter-spacing: .02em;
  font-weight: 400;
  box-sizing: border-box;
  padding-top: 16px;
}
.flex {
  display: flex;
  align-items: center;
  justify-content: center;
}
.center{
  margin: 1rem auto;
  width: 100%;
}
</style>
