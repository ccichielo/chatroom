<script lang="ts">
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();
	let message: string = '';

	const handleSubmit = (event: Event) => {
		event.preventDefault();
		if (message.trim()) {
			dispatch('sendMessage', message);
			message = '';
		}
	};
</script>

<form on:submit={handleSubmit} class="chat-input">
	<input type="text" bind:value={message} placeholder="Say something..." />
	<button type="submit">Send</button>
</form>

<style>
	.chat-input {
		display: flex;
		padding: 10px;
		border-top: 1px solid #ccc;
		background-color: #f9f9f9;
	}

	.chat-input input {
		flex: 1;
		padding: 10px;
		border: 1px solid #ccc;
		border-radius: 5px;
	}

	.chat-input button {
		margin-left: 10px;
		padding: 10px;
		border: none;
		border-radius: 5px;
		background-color: #007bff;
		color: white;
		cursor: pointer;
	}
</style>
