<script>
    export let type = "text";
    export let withLabel = true;
    export let labelText = "";
    export let inputModal = false;
    export let value = "";
    export let options = [];
</script>

{#if withLabel}
    <label for="" class="input-label"
        >{labelText}
        {@html $$props.required ? '<span class="text-red">*</span>' : ""}</label
    >
{/if}

{#if type == "text"}
    <input
        type="text"
        class={`input ${$$props.class}`}
        class:input-modal={inputModal}
        placeholder={$$props.placeholder}
        on:keyup
        bind:value
    />
{/if}

{#if type == "textarea"}
    <textarea
        class={`input ${$$props.class}`}
        class:input-modal={inputModal}
        placeholder={$$props.placeholder}
        cols="30"
        rows="5"
        on:input
        bind:value
    />
{/if}

{#if type == "select"}
    <select
        class={`input ${$$props.class}`}
        class:input-modal={inputModal}
        on:change
        bind:value
    >
        <option disabled selected value="">{$$props.placeholder}</option>
        {#each options as option, i (i)}
            <option value={option.toLowerCase()}>{option}</option>
        {/each}
    </select>
{/if}

<style>
    .input {
        padding: 0.9rem 1rem;
        font-size: 0.95em;
        display: inline-block;
        border: none;
        color: var(--gray-color-2);
        background-color: var(--white-color);
        width: 100%;
        border-radius: var(--border-radius);
        transition-property: outline, color;
        transition-duration: 0.3s;
        font-weight: var(--font-regular);
        border: 1px solid var(--gray-color);
    }

    textarea {
        resize: vertical;
    }

    .input:focus {
        color: var(--black-color);
    }

    .input-modal {
        background-color: var(--white-color-2);
    }
</style>
