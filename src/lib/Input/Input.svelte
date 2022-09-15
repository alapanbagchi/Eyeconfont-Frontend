<script lang="ts">
	export let label: string;
	export let name: string;
	export let type: 'text' | 'number' | 'email' | 'password' = 'text';
	export let placeholder: string;
	export let error: any;
	export let value: string;
	export let change: (event: Event) => void;
	let touched: boolean = false;
	function typeAction(node: { type: string }) {
		node.type = type;
	}
	const errorValidateAction = (e: any) => {
		if (e.target.value != '') touched = true;
		if (touched) change;
	};
</script>

<label class="label  {error ? 'error' : ''}">
	{label}

	<input
		{name}
		on:blur={errorValidateAction}
		on:input={touched || error ? change : undefined}
		use:typeAction
		on:change={change}
		bind:value
		{placeholder}
	/>
	{#if error}
		<p class="error_description">{error}</p>
	{:else}
		<p class="error_description">&nbsp</p>
	{/if}
</label>

<style>
	.label {
		width: 100%;
		font-size: 0.9em;
		font-weight: 500;
	}
	input {
		width: 100%;
		font-size: 14px;
		outline: none;
		display: flex;
		align-items: center;
		background-color: var(--surface);
		padding: 12px 15px;
		border-radius: 7px;
		transition: all 0.2s ease-in-out;
		margin-top: 15px;
		border: 1px solid transparent;
		background-color: var(--input_background);
	}
	input:hover,
	input:focus {
		border: var(--input_hover_border);
		box-shadow: var(--input_boxshadow);
	}

	.error input {
		background-color: var(--input_error_background);
		color: var(--error);
	}
	.error input:hover,
	.error input:focus {
		border: var(--input_error_border);
		box-shadow: var(--input_error_boxshadow);
	}
	.error_description {
		color: var(--error);
		font-size: 1em;
		margin: 10px 0 15px 0;
	}
</style>
