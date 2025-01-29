<script lang="ts">
    import { LinkIcon } from "lucide-svelte";
    import { Button } from "$lib/components/ui/button";
    import { Tooltip, TooltipContent, TooltipTrigger } from "$lib/components/ui/tooltip";
	import svelteTilt from 'vanilla-tilt-svelte';
	import Device from 'svelte-device-info'

    let {
        profile,
    }: {
        profile: {
            name: string;
            bio: string;
            website: string;
            stats: {
                posts: number;
                followers: number;
                following: number;
            };
        };
    } = $props();

    // Sample mosaic images
    const mosaicImages = [
        { id: 1, src: "https://picsum.photos/200/300", alt: "Mosaic 1" },
        { id: 2, src: "https://picsum.photos/200/301", alt: "Mosaic 2" },
        { id: 3, src: "https://picsum.photos/500/400", alt: "Mosaic 3" },
        { id: 4, src: "https://picsum.photos/600/1200", alt: "Mosaic 4" },
        { id: 5, src: "https://picsum.photos/500/300", alt: "Mosaic 5" },
        { id: 6, src: "https://picsum.photos/200/600", alt: "Mosaic 6" },
    ];
</script>

<div class=	"mt-2">
	<div class="grid grid-cols-3 md:grid-cols-4 grid-rows-1 gap-2">
		{#if Device.isPhone}
			{#each mosaicImages.slice(0, 2) as image}
				<div class="aspect-square rounded-xl">
				<img src={image.src} alt={image.alt} class="h-full w-full object-cover rounded-xl" />
			</div>
			{/each}
			<div class="grid grid-cols-2 grid-rows-2 gap-2">
				{#each mosaicImages.slice(2, 3) as image}
					<div class="col-span-2 aspect-[2/1] rounded-xl">
						<img src={image.src} alt={image.alt} class="h-full w-full object-cover rounded-xl" />
					</div>
				{/each}
				{#each mosaicImages.slice(3, 5) as image}
					<div class="aspect-square rounded-xl">
						<img src={image.src} alt={image.alt} class="h-full w-full object-cover rounded-xl" />
					</div>
				{/each}
			</div>
	{:else}
		{#each mosaicImages.slice(0, 3) as image}
			<div class="aspect-square rounded-xl">
            <img src={image.src} alt={image.alt} class="h-full w-full object-cover rounded-xl" />
        </div>
    	{/each}
		<div class="grid grid-cols-2 grid-rows-2 gap-2">
			{#each mosaicImages.slice(3, 4) as image}
				<div class="col-span-2 aspect-[2/1] rounded-xl">
					<img src={image.src} alt={image.alt} class="h-full w-full object-cover rounded-xl" />
            	</div>
			{/each}
			{#each mosaicImages.slice(4, 6) as image}
				<div class="aspect-square rounded-xl">
					<img src={image.src} alt={image.alt} class="h-full w-full object-cover rounded-xl" />
				</div>
			{/each}
		</div>
	{/if}
</div>
    <!-- Profile Picture -->
    <div class="shrink-0 absolute top-[22vw] md:top-56 ml-6 md:ml-10">
        <div class="size-[25vw] md:size-56 rounded-full bg-purple-500"></div>
    </div>

    <!-- Profile Info -->
    <div class="flex flex-1 flex-col gap-6 mt-24 md:mt-32">
        <div class="flex flex-col gap-4 sm:flex-row sm:items-center">
            <!-- Username and Link -->
            <div class="flex items-center gap-2">
                <h1 class="text-xl font-semibold">{profile.name}</h1>
                <Tooltip>
                    <TooltipTrigger asChild>
                        <a href={`https://${profile.website}`} target="_blank">
                            <Button variant="ghost" size="icon" class="h-8 w-8">
                                <LinkIcon class="size-4" />
                            </Button>
                        </a>
                    </TooltipTrigger>
                    <TooltipContent>Visit website</TooltipContent>
                </Tooltip>
            </div>

            <!-- Stats for Desktop -->
            <div class="hidden gap-8 sm:flex">
                <div>
                    <span class="font-semibold">{profile.stats.posts}</span>
                    <span class="text-muted-foreground">posts</span>
                </div>
                <div>
                    <span class="font-semibold">{profile.stats.followers}</span>
                    <span class="text-muted-foreground">followers</span>
                </div>
                <div>
                    <span class="font-semibold">{profile.stats.following}</span>
                    <span class="text-muted-foreground">following</span>
                </div>
            </div>
        </div>

        <!-- Stats for Mobile -->
        <div class="flex gap-8 sm:hidden">
            <div class="text-center">
                <span class="font-semibold">{profile.stats.posts}</span>
                <span class="block text-sm text-muted-foreground">posts</span>
            </div>
            <div class="text-center">
                <span class="font-semibold">{profile.stats.followers}</span>
                <span class="block text-sm text-muted-foreground">followers</span>
            </div>
            <div class="text-center">
                <span class="font-semibold">{profile.stats.following}</span>
                <span class="block text-sm text-muted-foreground">following</span>
            </div>
        </div>

        <!-- Bio -->
        <div>
            <p class="font-medium">{profile.bio}</p>
            <a href={`https://${profile.website}`} target="_blank" class="text-blue-500 hover:underline">
                {profile.website}
            </a>
        </div>
    </div>
</div>