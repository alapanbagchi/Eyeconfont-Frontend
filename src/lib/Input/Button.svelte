<script lang="ts">
	export let color: string;
	export let onClick: () => void;
	export let widthFull: boolean = false;
	export let disabled: boolean = false;
</script>

<button
	{disabled}
	on:click={onClick}
	style="{widthFull
		? 'width: 100%'
		: 'padding: 12px 30px'}; border: 2px solid {color} ; background-color: {color}"><slot /></button
>

<style>
	button {
		color: #ffffff;
		font-size: 14px;
		padding: 12px 0;
		border-radius: 7px;
		border: none;
		cursor: pointer;
		transition: all 0.3s ease-in-out;
		font-weight: 600;
	}
	button:hover {
		background-color: transparent !important;
		color: black;
		transition: all 0.3s ease-in-out;
	}
	button:active {
		transform: scale(0.95);
		transition: all 0.3s ease-in-out;
	}
	button:disabled {
		background-color: #e0e0e0;
		color: #9e9e9e;
		cursor: not-allowed;
	}
</style>
