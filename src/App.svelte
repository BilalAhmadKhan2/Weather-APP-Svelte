<script>
	import axios from "axios";
	import { API_KEY, API_URL } from "./constants";
	import SearchBar from "./SearchBar.svelte";
	import TemperatureCard from "./WeatherCard.svelte";
	import WeatherData from "./WeatherData.svelte";
	import Forecast from "./Forecast.svelte";
	import TempChart from "./TempChart.svelte";

	let query = "";
	let currentWeather = null;
	let forecastData = [];
	let errorMessage = null;
	let loading = false; 
	let eightTemps = [];
	let nineTemps = [];

	const dateToWords = (localtime) => {
		const months = [
			"January",
			"February",
			"March",
			"April",
			"May",
			"June",
			"July",
			"August",
			"September",
			"October",
			"November",
			"December",
		];

		const [date, time] = localtime.split(" ");
		const [year, month, dateNum] = date.split("-");
		const wordDate = `${
			months[parseInt(month, 10) - 1]
		} ${dateNum}, ${year}`;

		return `${wordDate} ${time}`;
	};

	const search = async () => {
		loading = true;
		const currentWeatherUrl = `${API_URL}?key=${API_KEY}&q=${query}&days=7&aqi=yes&alerts=no`;

		try {
			const response = await axios.get(currentWeatherUrl);
			const { current, location } = response.data;
			if (current && location) {
				currentWeather = { ...current, location: location };
				forecastData = response.data.forecast
					? response.data.forecast.forecastday
					: [];
				errorMessage = null;
			} else {
				throw new Error("Location or weather data not found");
			}

			eightTemps =
				forecastData.length > 0
					? forecastData[0].hour
							.map((hour) => hour.temp_c)
							.filter((_, i) => i % 3 === 0)
					: [];
			nineTemps = [
				...eightTemps,
				forecastData.length > 0
					? forecastData[0].hour[forecastData[0].hour.length - 1]
							.temp_c
					: null,
			];
		} catch (error) {
			console.log("Error:", error);
			errorMessage = error.message;
			currentWeather = null;
			forecastData = [];
		} finally {
			loading = false;
		}
	};
</script>

<div class="App fontstyle">
	<header class="py-3 custom-bg-color">
		<nav
			class="navbar navbar-expand container justify-content-between custom-bg-color"
		>
			<SearchBar bind:query {search} />
		</nav>
	</header>

	<div class="mb-4">
		{#if loading}
			<p class="load-message">Loading...</p>
		{/if}
		{#if errorMessage}
			<p class="error-message">{errorMessage}</p>
		{/if}
	</div>

	{#if currentWeather}
		<div class="container">
			<div class="row">
				<div class="col-lg-6 current-weather">
					<TemperatureCard
						type="temperature"
						cityName={currentWeather.location.name}
						region={`${currentWeather.location.region}/${currentWeather.location.country}`}
						localTime={dateToWords(
							currentWeather.location.localtime
						)}
						temperature={currentWeather.temp_c.toFixed(2)}
						temperatureUnit="°C"
						icon={`http:${currentWeather.condition.icon}`}
						condition={currentWeather.condition.text}
					/>
				</div>
				<div class="col-lg-6 forecast-container">
					<Forecast {forecastData} />
				</div>
			</div>
			<WeatherData weatherData={currentWeather} />

			<div class="row">
				<div class="col-12 mb-4">
					<TempChart {nineTemps} />
				</div>
			</div>
		</div>
	{/if}

	<footer class="py-3 custom-bg-color text-center text-white">
		<div class="container">
			<p>
				&copy; {new Date().getFullYear()} Weather App. All rights reserved.
				Designed and build by Bilal Ahmad Khan with Svelte, Bootstrap, CSS,
				Chart.js and WeatherAPI.
			</p>
		</div>
	</footer>
</div>

<style>

	.error-message {
		width: 100%;
		text-align: center; 
		margin-top: 10px; 
		color: red; 
	}
	.load-message {
		width: 100%;
		text-align: center; 
		margin-top: 10px; 
		color: rgb(30, 0, 255); 
	}

	.forecast-container {
		display: flex;
		justify-content: center;
		align-items: center;
	}
	.App {
		background-color: #00b4cc;
	}

	.custom-bg-color {
		background-color: #00b4cc;
	}
</style>

