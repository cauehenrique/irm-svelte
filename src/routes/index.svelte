<script lang="ts">
	import Message from "$lib/Message.svelte";
	import SettingsButton from "$lib/SettingsButton.svelte";
	import { io } from "socket.io-client";

	interface IMessage {
		hour: string;
		author: string;
		authorColor: string;
		message: string;
	}

	let settingsVisible = true;
	let messages: IMessage[] = [];

	let author = "";

	let authorColor = "#" + Math.floor(Math.random() * 16777215).toString(16);
	let message = "";

	let chatHistoryElement: HTMLElement;

	const socket = io("http://localhost:1337", { transports: ["websocket"] });

	socket.on("new-message", (newMessage) => {
		messages = [...messages, newMessage];
		if (chatHistoryElement) chatHistoryElement.scrollTop = chatHistoryElement.scrollHeight;
	});

	socket.on("new-user", (newUser) => {
		messages = [...messages, newUser];
	});

	function onSubmit() {
		if (message !== "" && author !== "") {
			const localeHour = new Date().toLocaleTimeString("pt-BR").split(":");
			const hour = `${localeHour[0]}:${localeHour[1]}`;

			socket.emit("new-message", { hour, author, authorColor, message });

			message = "";
		}
	}
</script>

<div class="h-screen flex justify-center items-center font-mono">
	<div
		class="border border-neutral-200 shadow-sm max-w-2xl w-full h-full md:h-auto md:max-h-96 flex flex-col justify-between"
	>
		<div class="flex flex-col p-2 h-full md:h-64 overflow-y-auto" bind:this={chatHistoryElement}>
			{#each messages as message, i (i)}
				<Message
					hour={message.hour}
					author={message.author.toLocaleLowerCase().replace(" ", "_")}
					authorColor={message.authorColor}
					message={message.message}
				/>
			{/each}
		</div>
		<div class="border-t border-neutral-200 flex">
			<SettingsButton bind:visible={settingsVisible} bind:color={authorColor} bind:name={author} />
			<form class="w-full" on:submit|preventDefault={onSubmit}>
				<input type="text" class="w-full p-2" bind:value={message} />
			</form>
		</div>
	</div>
</div>
