<script lang="ts">
    import { LinkIcon } from "lucide-svelte";
    import { Button } from "$lib/components/ui/button";
    import { Tooltip, TooltipContent, TooltipTrigger } from "$lib/components/ui/tooltip";

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
        { id: 1, src: "https://svelte0.dev/images/ui-placeholder.png", alt: "Mosaic 1" },
        { id: 2, src: "https://svelte0.dev/images/ui-placeholder.png", alt: "Mosaic 2" },
        { id: 3, src: "https://svelte0.dev/images/ui-placeholder.png", alt: "Mosaic 3" },
    ];
</script>

<!-- Mosaic Images -->
<div class="grid grid-cols-3 gap-0.5">
    {#each mosaicImages as image}
        <div class="aspect-[3/1]">
            <img src={image.src} alt={image.alt} class="h-full w-full object-cover" />
        </div>
    {/each}
</div>

<!-- Profile Section -->
<div class="flex gap-8 p-8">
    <!-- Profile Picture -->
    <div class="shrink-0">
        <div class="size-36 rounded-full bg-purple-500"></div>
    </div>

    <!-- Profile Info -->
    <div class="flex flex-1 flex-col gap-6">
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