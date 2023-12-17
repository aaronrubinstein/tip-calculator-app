<script>
    import { tick } from 'svelte';
    
    export let name;
    export let label;
    export let type = 'number';
    export let step = '1';
    export let min = '0';
    export let placeholder = '';
    export let icon;
    export let invalidMessage = '';
    export let value;
    
    let invalid = false;
    let input;
    export async function validateInput() {
        await tick();
        input.checkValidity() ? invalid = false : invalid = true;
    }
</script>

<div class="input-container">
    <div class="label-container">
        <label for="{name}">{label}</label>
        {#if invalid}
            <span>{invalidMessage}</span>
        {/if}
    </div>
    <input
        {...{ type }}
        {name}
        id={name}
        {placeholder}
        bind:value
        {step}
        {min}
        class:invalid 
        style="background-image: url({icon});"
        bind:this={input}
        on:input={validateInput} >
</div>

<style>
    .label-container {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 6px;
    }

    label, span {
        font-size: 16px;
        font-weight: 700;
    }

    label {
        color: var(--label);
    }

    span {
        color: var(--invalid);
    }

    input {
        height: 48px;
        width: 100%;
        border-radius: 5px;
        padding: 0 17px;
        font-size: 24px;
        font-weight: 700;
        text-align: right;
        color: var(--dark);
        background-color: var(--input-bg);
        background-position: 20px 16px;
        background-repeat: no-repeat;
        background-origin: border-box;
        border: none;
        outline: none;
    }

    input::placeholder {
        opacity: 0.35;
    }

    input:focus {
        border: 2px solid var(--primary);
    }

    input:invalid {
        border: 2px solid var(--invalid); 
    }

</style>         