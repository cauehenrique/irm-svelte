<script lang="ts">
	export let author: string;
	export let message: string;
	export let hour: string;
	export let authorColor: string;
</script>

<div class="block">
	<span class="text-neutral-400">{hour}</span>
	<span class="font-bold" style={`color: ${authorColor};`}>&lt;{author}&gt;</span>
	<span class="break-words">{message}</span>
</div>
