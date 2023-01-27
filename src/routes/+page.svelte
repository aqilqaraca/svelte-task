<script>
	import { get } from 'svelte/store';
	import Modal from './Modal.svelte';
	import { slide } from 'svelte/transition';
	import {
		carBrand,
		zipCode,
		carModel,
		errorMessage,
		firstName,
		firstRegistration,
		lastName
	} from './store';
	import { goto } from '$app/navigation';

	let formStep = 1;
	let showModal = false;
	let progressModal = false;
	let loading = true;
	let progress = 0;
	let redirectTo = null;

	function handleNext() {
		if (formStep === 1) {
			if (!validate()) {
				showModal = true;
				return;
			}
		}
		formStep++;
		errorMessage.set('');
	}

	function handleBack() {
		formStep--;
		errorMessage.set('');
	}

	function validate() {
		if (!get(carBrand).match(/^(Audi|BMW|Nissan)$/)) {
			errorMessage.set('Invalid car brand. Please enter Audi, BMW, or Nissan.');
			return false;
		}

		if (!get(zipCode).match(/^(65000|66000|67000|68000)$/)) {
			errorMessage.set('Invalid zip code. Please enter 65000, 66000, 67000, or 68000.');
			return false;
		}
		return true;
	}

	async function handleNext2() {
		if (formStep === 2) {
			if (!validate2()) {
				showModal = true;
				return;
			}
		}
		progressModal = true;
		while (progress < 100) {
			progress += 10;
			await new Promise((resolve) => setTimeout(resolve, 600));
		}
		loading = false;
		progressModal = false;
		redirectTo = Math.random() > 0.5 ? 'ResultV1' : 'ResultV2';
		goto(redirectTo);
		errorMessage.set('');
	}

	function validate2() {
		if (!get(firstName)) {
			errorMessage.set('Invalid first name. Please enter your first name.');
			return false;
		}
		if (!get(lastName)) {
			errorMessage.set('Invalid last name. Please enter your last name.');
			return false;
		}
		if (!get(carModel)) {
			errorMessage.set('Invalid car model. Please enter your car model.');
			return false;
		}
		if (!get(firstRegistration)) {
			errorMessage.set('Invalid first registration. Please enter your first registration.');
			return false;
		}
		return true;
	}
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
	{#if progressModal}
		<div class="progress">
			{#if loading}
				<div>
					Loading... {progress}%
					<progress value={progress} max="100" />
				</div>
			{/if}
		</div>
	{/if}

	<div class="form-wrapper">
		{#if formStep === 1}
			<form>
				<h2 class="form-title">Form #1</h2>
				<label>
					Car Brand:
					<input type="text" bind:value={$carBrand} />
				</label>
				<label>
					Zip Code:
					<input type="text" bind:value={$zipCode} />
				</label>
				<button on:click={handleNext}>Next</button>
			</form>
		{/if}

		{#if formStep === 2}
			<form transition:slide>
				<h2 class="form-title">Form #2</h2>
				<label>
					First Name:
					<input type="text" bind:value={$firstName} />
				</label>
				<label>
					Last Name:
					<input type="text" bind:value={$lastName} />
				</label>
				<label>
					Car Model:
					<input type="text" bind:value={$carModel} />
				</label>
				<label>
					First Registration:
					<input type="text" bind:value={$firstRegistration} />
				</label>
				<button on:click={handleBack}>Back</button>
				<button on:click={handleNext2}>Next</button>
			</form>
		{/if}

		{#if showModal}
			<Modal on:close={() => (showModal = false)}>
				<h2 class="error-message">{get(errorMessage)}</h2>
			</Modal>
		{/if}
	</div>
</section>
