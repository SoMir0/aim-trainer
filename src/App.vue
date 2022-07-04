<script lang="ts">
  import { defineComponent } from 'vue'
  let colors = ['blue', 'yellow', 'blueviolet', 'orange', 'brown', 'white', 'chocolate', 'purple', 'pink', 'chartreuse', 'maroon', 'aqua', 'green', 'gray', 'red'];
  let i = 0;

  export default defineComponent ({
    data() {
      return {
        x: '45%',
        y: '30%',
        bc: 'red',
        points: 0,
        misses: 0,
        clicks: 0,
        lastTime: Date.now(),
        speed: 0,
        precision: 0,
        best: 9999999,
        average: 0
      }
    },
    methods: {
      moveCircle: function() {
        this.x = Math.floor(Math.random() * 92) + '%';
        this.y = Math.floor(Math.random() * 92) + '%';
        this.points++;
        let newTime = Date.now();
        this.speed = newTime - this.lastTime;
        this.lastTime = newTime;
        this.precision = Math.floor((this.points/(this.misses+this.points))*100);
        this.clicks = this.points+this.misses;
        if(this.speed < this.best) this.best = this.speed;
        this.average += this.speed;
      },
      handleClick: function() {
        this.misses++;
        this.clicks = this.points+this.misses;
        this.precision = Math.floor((this.points/this.clicks)*100);
      },
      changeColor: function() {
        this.bc = colors[i];
        i++; if(i >= colors.length) i = 0;
      },
    },
    created() {
      let self = this;
      window.addEventListener('keydown', (e) => { if(e.keyCode == 32) self.changeColor() });
    },
    destroyed() {
      let self = this;
      window.removeEventListener('keydown', (e) => { if(e.keyCode == 32) self.changeColor() });
    },
  })
</script>

<template>
  <p class="stats" v-if="points == 0">Click the red ball to start</p>
  <p class="stats" v-else>Clicks: {{ clicks }}<br/>Speed: {{ speed }}ms<br/>Precision: {{ precision }}%<br/>[Spacebar to change color]</p>
  <p class="pb" v-show="points != 0">Best time: {{ best }}ms<br />Average: {{ Math.floor(average/points) }}ms</p>
  <div class="circle" :style="{background: bc, left: x, top: y}" @click="moveCircle()" v-click-outside="handleClick"></div>
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
  width: 5vmin; height: 5vmin;
  position: absolute;
  transition: 300ms;
}

.stats {
  color: #888;
  position: absolute; top: 50%; left: 50%;
  transform: translate(-50%, -50%);
}

.pb {
  color: #888;
  position: absolute; top: 50%; right: 5%;
  text-align: right;
  transform: translateY(-50%);
}
</style>
