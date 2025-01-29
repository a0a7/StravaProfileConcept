<script lang="ts">
	// Sample images data
	const images = Array.from({ length: 9 }, (_, i) => ({
		id: i + 1,
		src: "https://svelte0.dev/images/ui-placeholder.png",
		alt: `Instagram post ${i + 1}`,
	}));
</script>

<div class="grid grid-cols-3 gap-0.5">
	{#each images as image}
		<div class="aspect-square">
			<img src={image.src} alt={image.alt} class="h-full w-full object-cover" />
		</div>
	{/each}
</div>
