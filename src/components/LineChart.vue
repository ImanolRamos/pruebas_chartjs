<template lang="es">
    <line-chart-component
      :options="chartOptions"
      :data="chartData"
    />
  </template>
  
  <script>
  import { Line } from 'vue-chartjs'
  import { Chart as ChartJS, Title, Tooltip, Legend, LineElement, PointElement, LineController, CategoryScale, LinearScale, TimeScale } from 'chart.js'
  import 'chartjs-adapter-date-fns';

  ChartJS.register(Title, Tooltip, Legend, LineElement, PointElement, LineController, CategoryScale, LinearScale, TimeScale);
  
  export default {
    name: 'LineChart',
    components: {
      LineChartComponent: Line
    },
    data() {
      return {
        chartData: {
          labels: this.generateMinuteLabels(1440),
          datasets: [
            {
              label: 'Data One',
              backgroundColor: '#f87979',
              borderColor: '#f87979',
              data: this.generateRandomData(1440), // Datos para 24 horas con un punto por minuto (24 * 60)
              fill: false
            }
          ]
        },
        chartOptions: {
          responsive: true,
          maintainAspectRatio: false,
          scales: {
            x: {
              type: 'time',
              time: {
                unit: 'minute',
                displayFormats: {
                  minute: 'HH:mm'
                }
              },
              // ticks: {
              //   callback: function(value, index, values) {
              //     // Mostrar solo etiquetas de horas completas
              //     return index % 60 === 0 ? value : '';
              //   }
              // }
            }
          }
        }
      }
    },
    methods: {
      generateMinuteLabels(count) {
        // const labels = [];
        // for (let i = 0; i < 1440; i++) { // 1440 minutos en 24 horas
        //   const hours = Math.floor(i / 60).toString().padStart(2, '0');
        //   const minutes = (i % 60).toString().padStart(2, '0');
        //   labels.push(`${hours}:${minutes}`);
        // }
        // return labels;
        const labels = [];
        const startTime = new Date(); // Hora de inicio actual
        startTime.setHours(0, 0, 0, 0); // Establecer la hora a las 00:00

        for (let i = 0; i < count; i++) {
          const time = new Date(startTime.getTime() + i * 60000); // Avanzar un minuto
          labels.push(time);
        }
        return labels;



      },
      generateRandomData(count) {
        const data = [];
        for (let i = 0; i < count/2; i++) {
          data.push(Math.floor(Math.random() * 100));
        }
        for (let i = count/2; i < count; i++) {
          data.push(null);
        }
        return data;
      }
    }
  }
  </script>
  
  <style scoped>
  canvas {
    width: 100% !important;
    height: 100% !important;
  }
  </style>
  