<script lang="ts">
  export default {
    data: function() {
      return {
        x: '45%',
        y: '30%',
        points: 0
      }
    },
    methods: {
     moveCircle: function() {
       this.x = Math.floor(Math.random() * 92) + '%';
       this.y = Math.floor(Math.random() * 92) + '%';
       this.points++;
     },
    },
  }
</script>

<template>
  <p class="stats" v-if="points == 0">Click the red ball to start</p>
  <p class="stats" v-else>Score: {{points}}</p>
  <div class="circle red" :style="{left: x, top: y}" @click="moveCircle()"></div>
</template>

<style>
body {
  background: #111;
  user-select: none;
}

#app {
  font-family: 'monofur', monospace, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #eee;
  margin-top: 60px;
}

.circle {
  border-radius: 50%;
  width: 5vw; height: 5vh;
  position: absolute;
}

.stats {
  color: #444;
  position: absolute; top: 50%; left: 50%;
  transform: translate(-50%, -50%);
}

.red {
  background: red;
}
</style>
