<script lang="ts">
	export let visible = false;
	export let name: string;
	export let color = "#000000";
</script>

<button
	class="w-12 flex items-center justify-center border-r border-neutral-200 group hover:bg-neutral-100"
	on:click={() => (visible = true)}
>
	<svg
		xmlns="http://www.w3.org/2000/svg"
		viewBox="0 0 20 20"
		fill="currentColor"
		class="h-5 w-5 group-hover:text-neutral-800"
	>
		<path
			fill-rule="evenodd"
			clip-rule="evenodd"
			d="M11.49 3.17c-.38-1.56-2.6-1.56-2.98 0a1.532 1.532 0 01-2.286.948c-1.372-.836-2.942.734-2.106 2.106.54.886.061 2.042-.947 2.287-1.561.379-1.561 2.6 0 2.978a1.532 1.532 0 01.947 2.287c-.836 1.372.734 2.942 2.106 2.106a1.532 1.532 0 012.287.947c.379 1.561 2.6 1.561 2.978 0a1.533 1.533 0 012.287-.947c1.372.836 2.942-.734 2.106-2.106a1.533 1.533 0 01.947-2.287c1.561-.379 1.561-2.6 0-2.978a1.532 1.532 0 01-.947-2.287c.836-1.372-.734-2.942-2.106-2.106a1.532 1.532 0 01-2.287-.947zM10 13a3 3 0 100-6 3 3 0 000 6z"
		/>
	</svg>
</button>

{#if visible}
	<div class="fixed top-0 left-0 w-screen h-screen bg-black/50 flex items-center justify-center">
		<div class="p-4 bg-white rounded shadow-lg">
			{#if name}
				<div class="mb-2 flex justify-end">
					<button
						class="hover:bg-neutral-200 p-1 rounded-full"
						on:click={() => {
							visible = false;
							localStorage.setItem("author", name);
						}}
					>
						<svg
							xmlns="http://www.w3.org/2000/svg"
							viewBox="0 0 20 20"
							fill="currentColor"
							class="h-5 w-5 text-neutral-400"
						>
							<path
								fill-rule="evenodd"
								clip-rule="evenodd"
								d="M4.293 4.293a1 1 0 011.414 0L10 8.586l4.293-4.293a1 1 0 111.414 1.414L11.414 10l4.293 4.293a1 1 0 01-1.414 1.414L10 11.414l-4.293 4.293a1 1 0 01-1.414-1.414L8.586 10 4.293 5.707a1 1 0 010-1.414z"
							/>
						</svg>
					</button>
				</div>
			{/if}
			<div class="flex space-x-2">
				<input type="color" class="h-10" bind:value={color} />
				<input type="text" placeholder="Username" bind:value={name} />
			</div>
			<a
				href="https://github.com/cauehenrique/irm-svelte"
				target="_blank"
				class="bg-black hover:bg-neutral-700 text-white p-2 mt-2 rounded flex space-x-3 justify-center font-sans font-semibold items-center shadow-sm"
			>
				<svg width="20" height="20" viewBox="0 0 14 14">
					<path
						d="M7 .175c-3.872 0-7 3.128-7 7 0 3.084 2.013 5.71 4.79 6.65.35.066.482-.153.482-.328v-1.181c-1.947.415-2.363-.941-2.363-.941-.328-.81-.787-1.028-.787-1.028-.634-.438.044-.416.044-.416.7.044 1.071.722 1.071.722.635 1.072 1.641.766 2.035.59.066-.459.24-.765.437-.94-1.553-.175-3.193-.787-3.193-3.456 0-.766.262-1.378.721-1.881-.065-.175-.306-.897.066-1.86 0 0 .59-.197 1.925.722a6.754 6.754 0 0 1 1.75-.24c.59 0 1.203.087 1.75.24 1.335-.897 1.925-.722 1.925-.722.372.963.131 1.685.066 1.86.46.48.722 1.115.722 1.88 0 2.691-1.641 3.282-3.194 3.457.24.219.481.634.481 1.29v1.926c0 .197.131.415.481.328C11.988 12.884 14 10.259 14 7.175c0-3.872-3.128-7-7-7z"
						fill="currentColor"
						fill-rule="nonzero"
					/>
				</svg>
				<span>GitHub's Repository</span>
			</a>
		</div>
	</div>
{/if}

<style>
	input {
		@apply border border-neutral-300 px-3 py-2 rounded block shadow-sm;
	}
</style>
