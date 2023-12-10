<script>
	import Input from './lib/Input.svelte';
</script>

<img class="logo" src="images/logo.svg" alt="Splitter logo">
<main class="card">
	<Input 
		name="bill"
		label="Bill"
		type="number"
		step="0.01"
		placeholder="0"
		invalidMessage="Invalid amount"
		icon="images/icon-dollar.svg" />

	<Input 
		name="headcount"
		label="Number of People"
		type="number"
		placeholder="0"
		invalidMessage="Can't be zero"
		icon="images/icon-person.svg" />
</main>

<style>
	.logo {
		margin-top: 163px;
		margin-bottom: 87.86px;
	}

	.card {
		background: #FFF;
		max-width: 481px;
		border-radius: 25px;
		padding: 32px;
		padding-left: 48px;
	}
</style>
