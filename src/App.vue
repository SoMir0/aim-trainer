<script lang="ts">
  export default {
    data: function() {
      return {
        x: '45%',
        y: '30%'
      }
    },
    methods: {
     getUnits: function() {
       console.log('gsg');
     },
     moveCircle: function() {
       this.x = Math.floor(Math.random() * 92) + '%';
       this.y = Math.floor(Math.random() * 92) + '%';
     }
    },
    beforeMount() {
      this.getUnits();
    },
  }
</script>

<template>
  <p class="stats">Click the red ball to start</p>
  <div class="circle red" :style="{left: x, top: y}" v-on:click="moveCircle()"></div>
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
  width: 50px; height: 50px;
  position: absolute;
  top: 50%; left: 50px;
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
