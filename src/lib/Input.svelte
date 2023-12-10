<script>
    export let name;
    export let label;
    export let type = 'number';
    export let step = '1';
    export let min = '0';
    export let placeholder = '';
    export let icon;
    export let invalidMessage = '';

    let invalid = false;
</script>

<div class="input-container">
    <div class="label-container">
        <label for="{name}">{label}</label>
        {#if invalid}
            <span>{invalidMessage}</span>
        {/if}
    </div>
    <input
        type="{type}"
        {name}
        id={name}
        {placeholder}
        {step}
        {min}
        class:invalid 
        style="background-image: url({icon});" >
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

    /* Remove number input arrows/spinners */
    /* Chrome, Safari, Edge, Opera */
    input::-webkit-outer-spin-button,
    input::-webkit-inner-spin-button {
    -webkit-appearance: none;
    margin: 0;
    }

    /* Firefox */
    input[type=number] {
    -moz-appearance: textfield;
    }


</style>         