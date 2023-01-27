<script>
	import { get } from 'svelte/store';
	import { carBrand, firstName, lastName, carModel } from '../store';
</script>

<svelte:head>
	<title>ResultV2</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
	<h1>Result</h1>
	<div class="result-container">
		<div class="result-item">
			<h2>FullName</h2>
			<p>{`${get(firstName)} ${get(lastName)}`}</p>
		</div>
		<div class="result-item">
			<h2>Car</h2>
			<p>{`${get(carModel)} ${get(carBrand)}`}</p>
		</div>
	</div>
	<a href="/">Back</a>
	<a href="/ResultV1">Next</a>
</section>

<style>
	section {
		display: flex;
		justify-content: center;
		align-items: center;
		flex-direction: column;
		height: 100vh;
	}
	.result-container {
		display: flex;
		flex-wrap: wrap;
		width: 80%;
	}

	.result-item {
		flex: 1;
		margin: 1rem;
		padding: 1rem;
		border: 1px solid gray;
		border-radius: 5px;
	}
</style>
