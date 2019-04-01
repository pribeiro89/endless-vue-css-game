<template>
    <div 
        v-if="create"
        class="enemy"
        :class="!stopAnimation ? 'enemy-animation' : ''" 
    ></div>
</template>

<script>
export default {
    props: [
        'stopAnimation',
        'eId'
    ],

    data: () => ({
        create: false
    }),

    mounted() {
        let self = this
        setTimeout(function() {
            self.create = true
        }, 1000)
        this.create = false
    },

    updated() {
        this.setPosition()
    },

    methods: {
        setPosition: function() {
            let el = document.getElementById('enemy'+this.eId)
            if (!el) return;
            if (Math.random() >= 0.5) {
                el.style.left = "16%"
            } else {
                el.style.right = "16%"
            }
        }
    }
}
</script>

<style scoped>
.enemy {
  position: absolute;
  top: -15%;
  width: 100px;
  height: 100px;
  background-image: url("./../assets/poopEmoji.png");
  background-size: contain;
  background-repeat: no-repeat;
  background-position: center;
}

.enemy-animation {
  -webkit-animation: slide 4s linear infinite;
}

@keyframes slide {
    from { top: -15%; }
    to { top: 100%; }
}
</style>
