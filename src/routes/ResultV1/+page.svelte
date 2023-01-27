<script>
	import { get } from 'svelte/store';
	import { carBrand, zipCode, firstName, lastName, carModel, firstRegistration } from '../store';
</script>

<svelte:head>
	<title>ResultV1</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
	<h1>Result</h1>
	<div class="result-container">
		<div class="result-item">
			<h2>Car Brand</h2>
			<p>{get(carBrand)}</p>
		</div>
		<div class="result-item">
			<h2>Zip Code</h2>
			<p>{get(zipCode)}</p>
		</div>
		<div class="result-item">
			<h2>First Name</h2>
			<p>{get(firstName)}</p>
		</div>
		<div class="result-item">
			<h2>Last Name</h2>
			<p>{get(lastName)}</p>
		</div>
		<div class="result-item">
			<h2>Car Model</h2>
			<p>{get(carModel)}</p>
		</div>
		<div class="result-item">
			<h2>First Registration</h2>
			<p>{get(firstRegistration)}</p>
		</div>
	</div>
	<a href="/">Back</a>
	<a href="/ResultV2">Next</a>
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
