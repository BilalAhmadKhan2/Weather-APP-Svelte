<script>
    import WeatherCard from './WeatherCard.svelte';
    export let weatherData;
    const pressureIcon = 'https://icons.veryicon.com/png/o/miscellaneous/intelligent-agriculture/pressure-1.png';
  const humidityIcon = 'https://cdn-icons-png.flaticon.com/512/727/727790.png';
  const windspeedIcon = 'https://icon-library.com/images/wind-speed-icon/wind-speed-icon-6.jpg';
  const uvindexIcon = 'https://cdn-icons-png.flaticon.com/512/3262/3262975.png';
  const winddirIcon = 'https://cdn-icons-png.flaticon.com/512/2830/2830040.png';
  const airqualityIcon = 'https://cdn-icons-png.flaticon.com/512/5024/5024476.png';
  const feelslikeIcon = 'https://static-00.iconduck.com/assets.00/temperature-feels-like-icon-495x512-ylzv705f.png';
  const visibilityIcon = 'https://cdn-icons-png.flaticon.com/512/3395/3395544.png';
</script>
  
  <style>


  </style>
  
  <h3>Weather Details</h3>
  <div class="row">
    <div class="col-lg-3 mb-3">
        <WeatherCard title="Pressure" value={weatherData.pressure_mb} symbol="mb" type="weather" icon={pressureIcon}/>
      </div>
    <div class="col-lg-3 mb-3">
      <WeatherCard title="Humidity" value={weatherData.humidity} symbol="%" type="weather" icon={humidityIcon}/>
    </div>
    <div class="col-lg-3 mb-3">
      <WeatherCard title="Wind Speed" value={weatherData.wind_kph} symbol="kph" type="weather" icon={windspeedIcon}/>
    </div>
    <div class="col-lg-3 mb-3">
      <WeatherCard title="UV Index" value={weatherData.uv} symbol="" type="weather" icon={uvindexIcon}/>
    </div>
    <div class="col-lg-3 mb-3">
      <WeatherCard title="Wind Direction" value={weatherData.wind_dir} symbol="" type="weather" icon={winddirIcon}/>
    </div>
    <div class="col-lg-3 mb-3">
      <WeatherCard title="Air Quality Index (UK)" value={weatherData.air_quality['gb-defra-index']} symbol="" type="weather" icon={airqualityIcon}/>
    </div>
    <div class="col-lg-3 mb-3">
      <WeatherCard title="Feels Like" value={weatherData.feelslike_c.toFixed(2)} symbol="°C" type="weather" icon={feelslikeIcon}/>
    </div>
    <div class="col-lg-3 mb-3">
      <WeatherCard title="Visibility" value={weatherData.vis_km} symbol="km" type="weather" icon={visibilityIcon}/>
    </div>
  </div>
  