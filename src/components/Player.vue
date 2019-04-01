<template>
  <div 
    id="player" 
    class="player" 
  ></div>
</template>

<script>
import _ from 'lodash'

export default {
  name: 'Player',

  created() {
    window.addEventListener('keyup', (e) => {
      if (e.key == 'ArrowLeft') {
        this.moveLeft()
      }
      if (e.key == 'ArrowRight') {
        this.moveRight()
      }
    })
  },

  methods: {
    moveLeft: _.debounce(function(e) {
      document.getElementById('player').style.left = "16%";
      document.getElementById('player').style.right = "";
    }, 100),

    moveRight: _.debounce(function(e) {
      document.getElementById('player').style.left = "";
      document.getElementById('player').style.right = "16%";
    }, 100)
  }
}
</script>

<style scoped>
.player {
  position: absolute;
  background-image: url("./../assets/Celso.png");
  background-size: contain;
  background-repeat: no-repeat;
  background-position: center;
  right: 16%;
  bottom: 0%;
  
  width: 100px;
  height: 100px;
  
  -webkit-animation: rotate-90-ccw 0.15s linear infinite alternate both;
	        animation: rotate-90-ccw 0.15s linear infinite alternate both;
}

@-webkit-keyframes rotate-90-ccw {
  0% {
    -webkit-transform: rotate(-15deg);
            transform: rotate(-15deg);
  }
  100% {
    -webkit-transform: rotate(15deg);
            transform: rotate(15deg);
  }
}
@keyframes rotate-90-ccw {
  0% {
    -webkit-transform: rotate(-15deg);
            transform: rotate(-15deg);
  }
  100% {
    -webkit-transform: rotate(15deg);
            transform: rotate(15deg);
  }
}
</style>
