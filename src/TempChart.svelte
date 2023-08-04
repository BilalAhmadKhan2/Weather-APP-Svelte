<script>
    import { onMount, afterUpdate } from 'svelte';
    import Chart from 'chart.js/auto';
  
    export let nineTemps = [];
  
    const labels = ["00:00", "03:00", "06:00", "09:00", "12:00", "15:00", "18:00", "21:00", "24:00"];
    let chart;
  
    onMount(() => {
      const canvas = document.getElementById('temp-chart-canvas');
      const ctx = canvas.getContext('2d');
  
      const newArray = nineTemps;
  
      const newData = {
        labels,
        datasets: [
          {
            
            tension: 0.35,
            label: "Temperature (°C)",
            data: newArray,
            borderColor: "#FF0000",
            backgroundColor: "rgba(73, 133, 224, 0.5)",
            borderWidth: 5,
            radius: 3,
            hoverRadius: 10,
            hitRadius: 100,
            pointStyle: "circle",
            color: "#fff",
          },
        ],
      };
  
      const options = {
        scales: {
          y: {
            display: false,
            color: "#fff",
          },
          x: {
            border: {
              display: false,
              width: 10,
            },
            grid: {
              display: true,
              color: "rgba(255, 255, 255, 0.1)",
            },
            ticks: {
              color: "#fff",
              font: {
                family: '"Fira Sans", sans-serif',
                weight: 600,
                size: 15,
              },
            },
          },
        },
        responsive: true,
        plugins: {
          tooltip: {
            enabled: true,
            backgroundColor: "rgba(0, 0, 0, 0.8)",
            titleFont: {
              family: '"Fira Sans", sans-serif',
              size: 15,
            },
            bodyFont: {
              family: '"Fira Sans", sans-serif',
              size: 15,
            },
            padding: 20,
            caretSize: 10,
            displayColors: false,
          },
          legend: {
            display: true,
            position: "bottom",
            title: {
              display: false,
              text: "Yes",
              color: "#000",
            },
            strokeStyle: "#000",
            labels: {
              color: "#fff",
              padding: 20,
              font: {
                family: '"Fira Sans", sans-serif',
                weight: 600,
                size: 25,
              },
              pointStyle: "line",
              usePointStyle: true,
              pointStyleWidth: 0.001,
            },
          },
          title: {
            display: false,
            text: "Weather Chart",
          },
        },
      };
  
      chart = new Chart(ctx, {
        type: "line",
        data: newData,
        options,
      });
    });
  

    afterUpdate(() => {
      const newArray = nineTemps;
  
      chart.data.datasets[0].data = newArray;
      chart.update();
    });
  </script>
  
  <style>
    .temp-chart {
      background-color: rgba(0, 0, 0, 0.2);
      margin: 0 auto;
      padding: 50px;
      border-radius: 20px;
      max-width: 100%;
      width: 1270px;
    }
  
    @media only screen and (max-width: 720px) {
      .temp-chart {
        margin: 0;
        padding: 40px 30px;
        max-width: 100%;
        width: 500px;
      }
    }
  
    @media only screen and (max-width: 560px) {
      .temp-chart {
        /* margin-top: -60px; */
        padding: 40px 30px;
        max-width: 100%;
        width: 260px;
        /* scale: 0.57; */
      }
    }
    .temp-chart-heading {
    font-size: 32px;
    font-weight: bold;
    text-align: center;
    margin-bottom: 20px;
  }
  </style>
  
  <div class="temp-chart">
    <div class="temp-chart-heading">Hourly Forecast</div>
    <canvas id="temp-chart-canvas"></canvas>
  </div>
  