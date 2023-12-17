<script>
	import { createEventDispatcher } from "svelte";

	export let tip;
	export let total;
	export let disableReset;

	const dispatch = createEventDispatcher();
	const reset = () => dispatch('reset');

</script>

<div class="card">
	<div class="row">
		<div class="labels">
			<span class="main-label">Tip Amount</span>
			<span class="sub-label">/ person</span>
		</div>
		<span class="value">
			${(isFinite(tip) ? tip : 0)
				.toLocaleString('en', {minimumFractionDigits: 2, maximumFractionDigits: 2})}
		</span>
	</div>
	<div class="row">
		<div class="labels">
			<span class="main-label">Total</span>
			<span class="sub-label">/ person</span>
		</div>
		<span class="value">
			${(isFinite(total) ? total : 0)
				.toLocaleString('en', {minimumFractionDigits: 2, maximumFractionDigits: 2})}
		</span>
	</div>
	<button disabled={disableReset} on:click={reset} type="button">Reset</button>
</div>

<style>
    .card {
		display: flex;
		flex-direction: column;
		gap: 25px;
		height: 417px;
		width: 413px;
		background: var(--dark);
		border-radius: 15px;
		padding: 40px;
	}

	.row {
		display: flex;
		justify-content: space-between;
		align-items: center;
	}

	.labels {
		display: flex;
		flex-direction: column;
	}

	.main-label {
		color: #FFF;
		font-size: 16px;
		font-weight: 700;
	}

	.sub-label {
		color: var(--per-person-label);
		font-size: 13px;
		font-weight: 700;
	}

	.value {
		color: var(--primary);
		font-size: 48px;
		font-weight: 700;
		letter-spacing: -1px;
		text-align: right;
	}

	button {
		margin-top: auto;
		height: 48px;
		border-radius: 5px;
		background: var(--primary);
		color: var(--dark);
		font-size: 20px;
		font-weight: 700;
		text-transform: uppercase;
		cursor: pointer;
	}

	button:hover {
		background: var(--btn-hover);
	}

	button:disabled {
		background: var(--disabled);
		color: var(--disabled-text);
	}

	@media (max-width: 960px) {
		.card {
			width: auto;
			height: 257px;
			padding: 37px 22px 24px 24px;
		}

		.value {
			font-size: 32px;
			letter-spacing: 0.667px;
		}
	}

</style>