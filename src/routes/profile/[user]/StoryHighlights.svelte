<script lang="ts">
	const highlights = [
		{ id: 1, name: "Highlight" },
		{ id: 2, name: "Highlight" },
		{ id: 3, name: "Highlight" },
		{ id: 4, name: "Highlight" },
	];
</script>

<div class="border-t">
	<div class="mx-auto max-w-screen-lg overflow-x-auto p-4">
		<div class="flex gap-4">
			{#each highlights as highlight}
				<div class="flex flex-col items-center gap-2">
					<div class="size-16 rounded-full bg-purple-500 p-0.5 ring-2 ring-border">
						<div class="size-full rounded-full bg-muted"></div>
					</div>
					<span class="text-sm">{highlight.name}</span>
				</div>
			{/each}
		</div>
	</div>
</div>
