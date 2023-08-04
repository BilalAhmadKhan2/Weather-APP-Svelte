<script>
  export let type;
  export let title = '';
  export let value = '';
  export let symbol = '';
  export let icon = null;
  export let cityName = '';
  export let region = '';
  export let localTime = '';
  export let temperature = '';
  export let temperatureUnit = '';
  export let condition = '';
</script>

<style>
  .weather-card {
    background-color: transparent;
    border: none;
    box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.1);
  }

  .weather-card .card-body {
    background-color: rgba(255, 255, 255, 0.9);
    border-radius: 8px;
    padding: 20px;
  }

  .temperature-card-left {
    flex: 1;
    border-right: 1px solid #000;
    padding-right: 10px;
    text-align: center;
  }

  .temperature-card-right {
    flex: 1;
    padding-left: 10px;
    text-align: left;
  }


  img.icon {
    width: 48px;
    height: 48px;
  }
</style>

{#if type === 'weather'}
  <div class="weather-card" style="width: 18rem;">
    <div class="card-body">
      <h5>{title}</h5>
      {#if icon}
        <img src={icon} alt={title} class="icon" />
      {/if}
      {#if value}
        <p>
          {value} {symbol}
        </p>
      {/if}
    </div>
  </div>
{:else if type === 'temperature'}
  <div class="weather-card" style="width: 18rem;">
    <div class="card-body">
      <div style="display: flex; flex-direction: row; justify-content: space-between;">
        <div class="temperature-card-left">
          {#if icon}
            <img src={icon} alt="Weather icon" style="width: 90px; height: 90px; margin-bottom: 10px;" />
          {/if}
          <div>
            <strong style="font-size: 1.5em;">{temperature} {temperatureUnit}</strong>
          </div>
        </div>
        <div class="temperature-card-right">
          {#if cityName}
            <h5 style="font-weight: bold; font-size: 1.2em; margin-bottom: 5px;">{cityName}</h5>
          {/if}
          {#if region}
            <h6>{region}</h6>
          {/if}
          {#if localTime}
            <h6>{localTime}</h6>
          {/if}
          {#if condition}
            <p>{condition}</p>
          {/if}
        </div>
      </div>
    </div>
  </div>
{/if}
