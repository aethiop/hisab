<script>
	// @ts-nocheck
	import Text from "$atoms/Text.svelte";
	import DownloadFile from "$molecules/DownloadFile.svelte";
	import Erase from "$molecules/Erase.svelte";
	import { files } from "$lib/store.js";
	import { onMount } from "svelte";
	import { fetchFiles } from "$lib/cloud.js";
	export let folder;
	onMount(() => {
		fetchFiles(folder);
	});
</script>

{#if $files.length > 0}
	<div
		class="flex overflow-hidden w-full p-2 items-center flex-col space-y-4"
	>
		{#each $files as { name, folder }}
			{#if folder.slice(0, 5) == "trash"}
				<Erase {name} {folder} />
			{:else}
				<DownloadFile {name} {folder} />
			{/if}
		{/each}
	</div>
{:else}
	<div
		class="w-full h-full font-bold tracking-widest flex justify-center items-center"
	>
		<Text type=" body ">No files here.</Text>
	</div>
{/if}
