<script>
	import Input from './lib/Input.svelte';
	import SummaryCard from './lib/SummaryCard.svelte';
	
	let bill;
	let people;
	let standardTip;
	let customTip;
	let disableReset = true;
	let billInput
	let numberInput
	
	$: tipPerPerson = bill * ((standardTip ?? customTip) / 100) / people;
	$: totalPerPerson = (Number(bill) + bill * ((standardTip ?? customTip) / 100)) / people;

	$: {
		let allFieldsEmpty = true;
		[bill, people, standardTip, customTip].forEach(field => {
			if (isFinite(field) && field !== '' && field !== null) {
				allFieldsEmpty = false;
			};
		});
		allFieldsEmpty ? disableReset = true : disableReset = false;
	}
	
	const reset = () => {
		bill = undefined;
		people = undefined;
		standardTip = undefined
		customTip = undefined;
		billInput.validateInput();
		numberInput.validateInput();
	};

</script>

<img class="logo" src="images/logo.svg" alt="Splitter logo">
<main class="card">
	<form>
		<Input 
			name="bill"
			label="Bill"
			type="number"
			bind:value={bill}
			step="0.01"
			placeholder="0"
			invalidMessage="Invalid amount"
			icon="images/icon-dollar.svg"
			bind:this={billInput} />
		
		<p>Select Tip %</p>

		<div class="tip-button-container">
			{#each [5, 10, 15, 25, 50] as tipOption}
				<label>
					<input 
						type="radio"
						name="tipOption"
						value={tipOption} 
						bind:group={standardTip}
						on:input={() => customTip = undefined} >
					<span>{tipOption}%</span>
				</label>
			{/each}
			<input 
				type="number"
				name="custom-tip"
				id="custom-tip"
				bind:value={customTip}
				placeholder="Custom"
				step="0.01"
				min="0"
				on:input={() => standardTip = undefined} >
		</div>
	
		<Input 
			name="headcount"
			label="Number of People"
			type="number"
			bind:value={people}
			placeholder="0"
			min="1"
			invalidMessage="Invalid number"
			icon="images/icon-person.svg"
			bind:this={numberInput} />
	</form>

	<SummaryCard 
		on:reset={reset} 
		{disableReset}
		tip={tipPerPerson} 
		total={totalPerPerson} />
</main>

<style>
	.logo {
		margin-top: 163px;
		margin-bottom: 87.86px;
	}

	.card {
		background: #FFF;
		max-width: 920px;
		border-radius: 25px;
		padding: 32px;
		padding-left: 48px;
		display: flex;
		gap: 48px;
		margin-bottom: 80px;
	}

	form {
		width: 379px;
	}

	p {
		font-size: 16px;
        font-weight: 700;
		color: var(--label);
		margin-top: 40px;
		margin-bottom: 16px;
	}

	.tip-button-container {
		display: grid;
		grid-template-columns: 1fr 1fr 1fr;
		grid-template-rows: 1fr 1fr;
		gap: 16px 14px;
		margin-bottom: 40px;
	}

	input[type="radio"] {
		position: absolute;
		opacity: 0;
		cursor: pointer;
		height: 0;
		width: 0;
	}

	span {
		display: grid;
		place-items: center;
		background: var(--dark);
		height: 48px;
		border-radius: 5px;
		font-size: 24px;
		font-weight: 700;
		color: #FFF;
		cursor: pointer;
	}

	span:hover {
		background: var(--btn-hover);
		color: var(--dark);
	}

	input[type="radio"]:checked + span {
		background: var(--primary);
		color: var(--dark);
	}

	input {
        height: 48px;
        width: 100%;
        border-radius: 5px;
        padding: 0 13px;
        font-size: 24px;
        font-weight: 700;
        text-align: right;
        color: var(--dark);
        background-color: var(--input-bg);
        border: none;
        outline: none;
    }
	
	input::placeholder {
        color: var(--custom-tip-placeholder)
    }

    input:focus {
        border: 2px solid var(--primary);
    }

    input:invalid {
        border: 2px solid var(--invalid); 
    }

	@media (max-width: 960px) {
		.logo {
			margin-top: 50px;
			margin-bottom: 40.86px;
		}

		.card {
			max-width: 600px;
			flex-grow: 1;
			border-radius: 25px 25px 0 0;
			padding: 32px;
			display: block;
			margin-bottom: 0px;
		}

		form {
			width: auto;
			margin-bottom: 32px;
		}

		p {
			margin-top: 32px;
		}

		.tip-button-container {
			grid-template-columns: 1fr 1fr;
			grid-template-rows: 1fr 1fr;
			gap: 16px 16.56px;
			margin-bottom: 32px;
		}
	}

</style>
