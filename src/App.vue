<template>
  <div id="app">
    <div id="bg" class="bg bg-animation">
      <Enemy 
        v-for="n in enemies" :key="n"
        :stopAnimation="gameOver"
        :id="`enemy${n}`"
        :eId="n"
      />
      <Player />
    </div>
    <div v-show="gameOver" class="gameover">
      Game Over!<br>
      <button @click="gameOver = false" class="try-again">Try again!</button>
    </div>
  </div>
</template>

<script>
import _ from 'lodash'
import Player from './components/Player.vue'
import Enemy from './components/Enemy.vue'
import { setInterval } from 'timers';

export default {
  name: 'app',
  components: {
    Player,
    Enemy
  },

  data: () => ({
    gameOver: false,
    enemies: 2
  }),

  mounted() {
    let self = this
    setInterval(function(e) {
      if (!self.gameOver) {
        self.reRender()
      }
    }, 50)
  },

  methods: {
    collide: function (el1, el2) {
      var rect1 = el1.getBoundingClientRect();
      var rect2 = el2.getBoundingClientRect();

      return !(
        rect1.top > rect2.bottom ||
        rect1.right < rect2.left ||
        rect1.bottom < rect2.top ||
        rect1.left > rect2.right
      );
    },

    reRender: function(e) {
      let player = document.getElementById('player')
      let enemyEl = document.getElementsByClassName('enemy')[0]
      if (enemyEl !== 'undefined') {
      // console.log(enemyEl)
        let r = this.collide(player, enemyEl)
        this.gameOver = r;
      }

      // if (r) {
      //   document.getElementById('bg').classList.toggle('bg-animation')
      // }
    },
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
  display: flex;
  justify-content: center;
}
html, 
body {
  margin: 0;
  padding: 0;
}

.gameover {
  font-weight: 700;
  font-size: 60px;
  position: absolute;
  z-index: 1;
  top: 50%;
  text-align: center;
}

.try-again {
  height: 60px;
  width: 150px;
  font-size: 20px;
  background-color: rgb(86, 205, 50);
  border-color: rgb(76, 184, 44);
}

.bg {
  position: relative;
  align-items: flex-end;
  background-image: url("./assets/bg.jpg");
  background-repeat: repeat-y;
  background-position: 0 0;
  width: 432px;
  height: 100vh;
  margin: 0;
}

.bg-animation {
  -webkit-animation: slide 5s linear infinite;
}

@keyframes slide {
    from { background-position: 0 -767px; }
    to { background-position: 0 0; }
}
</style>
