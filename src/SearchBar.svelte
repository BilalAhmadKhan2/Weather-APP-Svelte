<script>
	export let query;
	export let search = () => {};

	const handleQueryChange = (event) => {
		query = event.target.value;
	};
</script>

<style>
	@import url(https://fonts.googleapis.com/css?family=Open+Sans);

	/*body {
		background: #f2f2f2;
		font-family: 'Open Sans', sans-serif;
	}*/
	.search {
		width: 100%;
		max-width: 400px; 
		margin: 0 auto;
		position: relative;
		display: flex;
	}

	.searchTerm {
		width: 100%;
		border: 3px solid #00B4CC;
		border-right: none;
		padding: 5px;
		height: 36px; 
		border-radius: 5px 0 0 5px;
		outline: none;
		color: #9DBFAF;
	}

	.searchTerm:focus {
		color: #00B4CC;
	}

	.searchButton {
		width: 40px;
		height: 36px; 
		border: 1px solid #00B4CC;
		background: #00B4CC;
		text-align: center;
		color: #fff;
		border-radius: 0 5px 5px 0;
		cursor: pointer;
		font-size: 20px;
	}
</style>

<div class="search">
	<input
		type="text"
		bind:value={query}
		on:input={handleQueryChange}
		placeholder="Enter City Name"
		class="searchTerm"
	/>
	<button on:click={search} class="searchButton">
		<i class="fa fa-search"></i>
	</button>
</div>
