<script lang="ts">
    import { ExternalLinkIcon } from "lucide-svelte";
    import { Button } from "$lib/components/ui/button";
    import { Tooltip, TooltipContent, TooltipTrigger } from "$lib/components/ui/tooltip";
	import svelteTilt from 'vanilla-tilt-svelte';
	import Device from 'svelte-device-info'
    import { getContext } from 'svelte';
    import { onMount } from 'svelte';

    let isMobile = $state(false);

    onMount(() => {
        const checkMobile = () => {
            isMobile = window.matchMedia("(max-width: 768px)").matches;
        };

        checkMobile();
        window.addEventListener('resize', checkMobile);

        return () => {
            window.removeEventListener('resize', checkMobile);
        };
    });

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

<div class=	"lg:mt-2">
	<div class="grid grid-cols-3 md:grid-cols-4 grid-rows-1 gap-1 mb-36">
		{#if isMobile}
			{#each mosaicImages.slice(0, 2) as image}
				<div class="aspect-square rounded-xl">
				<img src={image.src} alt={image.alt} class="h-full w-full object-cover rounded-xl" />
			</div>
			{/each}
			<div class="grid grid-cols-2 grid-rows-2 gap-1">
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
		<div class="grid grid-cols-2 grid-rows-2 gap-1">
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
<div class="absolute top-[22vw] md:top-[17vw] lg:top-56 flex w-full">
    <!-- username & profile picture -->
    <div class="ml-[2vw] md:ml-[3vw] lg:ml-8 flex-shrink"> 
        <div class="size-[25vw] md:size-[13.5rem] lg:size-64 rounded-full bg-purple-500"></div>
        <!-- username -->
        <div class="flex items-center gap-1 ml-[2vw] md:ml-[3vw] lg:ml-8">
            <h1 class="text-[3rem] md:text-[3rem] font-semibold">{profile.name}</h1>
            <Tooltip>
                <TooltipTrigger asChild>
                    <a href={`https://${profile.website}`} target="_blank">
                        <Button variant="ghost" size="icon" class="h-8 w-8">
                            <ExternalLinkIcon class="size-4" />
                        </Button>
                    </a>
                </TooltipTrigger>
                <TooltipContent>Visit website</TooltipContent>
            </Tooltip>
        </div>
    </div>
    <!-- stats -->
    <div class="mt-36 grid grid-cols-3 grid-rows-1 flex-grow items-center justify-center gap-4">
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
<div>
    <p class="font-medium">{profile.bio}</p>
    <a href={`https://${profile.website}`} target="_blank" class="text-blue-500 hover:underline">
        {profile.website}
    </a>
</div>
</div>


            