<script lang="ts">
	import ChatWindow from '../components/ChatWindow.svelte';
	import Login from '../components/Login.svelte';

	let loggedIn = false;
	let username = '';

	const handleLogin = (event: CustomEvent<string>) => {
		username = event.detail;
		loggedIn = true;
	};
	const handleLogout = () => {
		username = '';
		loggedIn = false;
	};
</script>

<main>
	{#if !loggedIn}
		<Login on:login={handleLogin} />
	{:else}
		<button on:click={handleLogout}>Logout</button>
		<ChatWindow {username} />
	{/if}
</main>

<style>
	button {
		padding: 10px 20px;
		border: none;
		border-radius: 5px;
		background-color: #007bff;
		color: white;
		cursor: pointer;
	}
</style>
