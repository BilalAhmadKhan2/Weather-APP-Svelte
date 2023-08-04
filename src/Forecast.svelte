<script>
  export let forecastData = [];

  const getDayName = (dateString) => {
    const date = new Date(dateString);
    const days = ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"];
    return days[date.getDay()];
  };
</script>

<style>
  .fontstyle {
    font-family: 'Open Sans', sans-serif;
  }

  .bold-text {
    font-weight: bold;
  }

  .smaller-text {
    font-size: 0.7em; 
  }

  .card.forecast-card.fontstyle.weather-card {
    background-color: transparent;
    border: none;
    box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.1); 
  }

  .card-body.weather-card {
    background-color: rgba(255, 255, 255, 0.9); 
    border-radius: 8px;
    padding: 20px;
  }

</style>

<div class="card forecast-card fontstyle weather-card">
  <div class="card-body weather-card">
    <div class="row">
      {#each forecastData as forecast, index}
        <div class="col" style="width: calc(100% / 7);">
          <div class="forecast-day">
            <p class="forecast-date bold-text">{getDayName(forecast.date, index)}</p>
            <img src={`http:${forecast.day.condition.icon}`} alt={forecast.day.condition.text} class="forecast-icon" />
            <div class="forecast-temperature">
              <p class="smaller-text">H {forecast.day.maxtemp_c.toFixed(2)} °C</p>
              <p class="smaller-text">L {forecast.day.mintemp_c.toFixed(2)} °C</p>
            </div>
          </div>
        </div>
      {/each}
    </div>
  </div>
</div>

