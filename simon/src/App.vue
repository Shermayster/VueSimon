<template>
  <div id="app">
    <header>
      <span>Simon Game</span>
    </header>
    <div class="flex" :class="{menu: !gameStarted, gameStarted: gameStarted}">
        <transition name="fade">
          <div v-if="!gameStarted">
            <btn :btnData="startBtn" @clickEvent="startGame"></btn>
          </div>
        </transition>
        <transition name="fade">
          <div v-if="gameStarted">
            <btn @clickEvent="checkTurn(red.styleClass)" :btnData="red"></btn>
            <btn @clickEvent="checkTurn(blue.styleClass)" :btnData="blue"></btn>
            <btn @clickEvent="checkTurn(orange.styleClass)" :btnData="orange"></btn>
            <btn @clickEvent="checkTurn(green.styleClass)" :btnData="green"></btn>
        </div>
        </transition>
    </div>
  </div>
</template>

<script>
import Btn from './components/Button'

const btnClick = (selector) => {
  console.log('buttons clicked', `.${selector}`)
  const btn = document.querySelector(`.${selector}`)
  btn.classList.add('active')
  return new Promise((resolve) => {
    setTimeout(() => {
      btn.classList.remove('active')
      console.log('classed', btn.classList)
      resolve('')
    }, 1000)
  })
}

export default {
  name: 'app',
  components: {
    Btn
  },
  data () {
    return {
      red: {
        styleClass: ['btn-red'],
        name: 'Red'
      },
      blue: {
        styleClass: ['btn-blue'],
        name: 'Blue'
      },
      orange: {
        styleClass: ['btn-orange'],
        name: 'Orange'
      },
      green: {
        styleClass: ['btn-green'],
        name: 'Green'
      },
      startBtn: {
        styleClass: ['btn-blue'],
        name: 'Start Game'
      },
      round: 1,
      gameStarted: false,
      btnOrder: [],
      turn: 0
    }
  },
  methods: {
    aiTurn: function () {
      const buttons = ['btn-red', 'btn-blue', 'btn-orange', 'btn-green']
      if (this.btnOrder.length < this.round) {
        console.log('ai turn', this.round)
        const randNumber = Math.floor(Math.random() * 3)
        this.btnOrder.push(buttons[randNumber])
        btnClick(buttons[randNumber]).then(res => {
          setTimeout(() => {
            this.aiTurn()
          }, 1000)
        })
      }
    },
    startGame: function () {
      this.gameStarted = true
      setTimeout(() => {
        this.aiTurn()
      }, 2000)
    },
    checkTurn: function (e) {
      console.log('class')
      console.log('check', e[0] === this.btnOrder[this.turn])
      if (e[0] === this.btnOrder[this.turn]) {
        this.turn++
        if (this.turn >= this.round) {
          this.round++
          this.aiTurn()
          this.turn = 0
          this.btnOrder = []
        }
      } else {
        this.endGame()
      }
    },
    endGame: function () {
      console.log('end game ')
      this.gameStarted = false
      this.turn = 0
      this.round = 0
      this.btnOrder = []
    }
  }
}
</script>

<style lang="scss">
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
  flex-direction: row;
  flex-wrap: wrap;
}

.center {
  margin: 1rem auto;
  width: 100%;
}

.menu {
  background: #ecf0f1;
  height: 100vh;
}
.gameStarted {
  background: #fff;
}

.fade-leave-active {
  transition: opacity .5s;
  position: absolute;
}
.fade-enter-active {
  transition: opacity 1s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active in <2.1.8 */ {
  opacity: 0
}
</style>
