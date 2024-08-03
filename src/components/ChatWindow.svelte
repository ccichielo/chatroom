<script lang="ts">
	import ChatInput from './ChatInput.svelte';

	export let username: string = '';

	type Message = {
		user: string;
		text: string;
	};

	let messages: Message[] = [];
	let ws: WebSocket | null = null;

	function connectWebSocket() {
		if (!username) return;

		ws = new WebSocket('ws://localhost:8080/ws?username=' + encodeURIComponent(username));

		ws.onmessage = (event) => {
			const message = JSON.parse(event.data) as Message;
			messages = [...messages, message];
		};

		ws.onerror = (error) => {
			console.error('Websocket error:', error);
		};

		ws.onclose = () => {
			console.log('Websocket connection closed');
		};
	}

	const handleSendMessage = (event: CustomEvent<string>) => {
		const newMessage = event.detail;

		if (ws && newMessage.trim()) {
			ws.send(JSON.stringify({ user: username, text: newMessage }));
		}
	};

	$: if (username) {
		connectWebSocket();
	}
</script>

<div class="chat-box">
	{#each messages as { user, text }}
		<div class="message">
			<span class="user">{user}</span>
			<span class="text">{text}</span>
		</div>
	{/each}
</div>

<ChatInput on:sendMessage={handleSendMessage} />

<style>
	.chat-box {
		border: 1px solid #ccc;
		border-radius: 5px;
		max-height: 400px;
		overflow-y: auto;
		padding: 10px;
		background-color: #f9f9f9;
	}

	.message {
		margin-bottom: 10px;
	}

	.message .user {
		font-weight: bold;
	}

	.message .text {
		margin-left: 10px;
	}
</style>
