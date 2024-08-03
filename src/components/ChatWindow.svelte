<script lang="ts">
	import ChatInput from './ChatInput.svelte';

	export let username: string = '';

	type Message = {
		user: string;
		text: string;
	};

	let messages: Message[] = [
		{ user: 'Foo', text: 'Bar' },
		{ user: 'Foo', text: 'Bar' }
	];

	const handleSendMessage = (event: CustomEvent<string>) => {
		const newMessage = event.detail;
		messages = [...messages, { user: username, text: newMessage }];
	};
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
