<script lang="ts">
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();
	let username: string = '';
	function handleClick() {
		if (username.trim()) {
			dispatch('login', username);
		}
	}
</script>

<div class="login-container">
	<input id="username" type="text" placeholder="Username" bind:value={username} required />
	<button on:click={handleClick}> Login </button>
</div>

<style>
	.login-container {
		padding: 20px;
		text-align: center;
	}

	.login-container input {
		padding: 10px;
		margin: 5px;
		border: 1px solid #ccc;
		border-radius: 5px;
	}

	.login-container button {
		padding: 10px 20px;
		border: none;
		border-radius: 5px;
		background-color: #007bff;
		color: white;
		cursor: pointer;
	}
</style>
