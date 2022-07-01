<script lang="ts">
  export default {
    data: function() {
      return {
        x: '45%',
        y: '30%',
        points: 0,
        misses: 0,
        clicks: 0,
        lastTime: Date.now(),
        speed: 0,
        precision: 0
      }
    },
    methods: {
      moveCircle: function() {
        this.x = Math.floor(Math.random() * 92) + '%';
        this.y = Math.floor(Math.random() * 92) + '%';
        this.points++;
        let newTime: Date = Date.now();
        this.speed = newTime - this.lastTime;
        this.lastTime = newTime;
        this.precision = Math.floor((this.points/(this.misses+this.points))*100);
        this.clicks = this.points+this.misses;
      },
      handleClick: function() {
        this.misses++;
        this.clicks = this.points+this.misses;
        this.precision = Math.floor((this.points/this.clicks)*100);
      },
    },
  }
</script>

<template>
  <p class="stats" v-if="points == 0">Click the red ball to start</p>
  <p class="stats" v-else>Clicks: {{ clicks }}<br/>Speed: {{ speed }}ms<br/>Precision: {{ precision }}%</p>
  <div class="circle red" :style="{left: x, top: y}" @click="moveCircle()" v-click-outside="handleClick"></div>
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
  color: #888;
  position: absolute; top: 50%; left: 50%;
  transform: translate(-50%, -50%);
}

.red {
  background: red;
}
</style>
