<template lang="es">
  <div id="app">
    <div class="cabecera">
      <h1>Lista de tareas</h1>
    </div>
    <div class="graficas">
      <div class="chart-container">
        <BarChart />
      </div>
      <div class="chart-container">
        <LineChart />
      </div>
    </div>
  </div>
</template>

<script>
import BarChart from './components/BarChart.vue'
import LineChart from './components/LineChart.vue'


export default {
  name: 'App',
  components: {
    BarChart, LineChart
  }
}
</script>

<style>
html,
body {
  height: 100%;
  margin: 0;
}

#app {
  height: 100%;
  display: flex;
  flex-direction: column;
}

.cabecera {
  height: 20%;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #f0f0f0; /* color de fondo opcional para la cabecera */
}

.graficas {
  height: 80%;
  display: flex;
  flex-direction: column;
}

.chart-container {
  height: 50%; /* 50% of 80% makes it 40% of the total height */
}

canvas {
  width: 100% !important;
  height: 100% !important;
}
</style>
