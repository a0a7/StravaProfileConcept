<script lang="ts">
	import { Tabs, TabsList, TabsTrigger, TabsContent } from "$lib/components/ui/tabs";
	import { BetweenHorizontalEndIcon, UsersIcon } from "lucide-svelte";
	import ProfileHeader from "./ProfileHeader.svelte";
	import StoryHighlights from "./StoryHighlights.svelte";
	import PhotoGrid from "./PhotoGrid.svelte";

	// Profile data
	const profile = {
		name: "Name",
		bio: "Local business",
		website: "www.website.com",
		stats: {
			posts: 129,
			followers: 3680,
			following: 230,
		},
	};
</script>

<main class="min-h-screen w-full bg-background text-foreground">
	<div class="mx-auto max-w-screen-lg">
		<!-- Profile Header Section -->
		<ProfileHeader {profile} />

		<!-- Story Highlights -->
		<StoryHighlights />

		<!-- Posts Tabs -->
		<Tabs defaultValue="posts" class="w-full">
			<TabsList class="grid w-full grid-cols-2">
				<TabsTrigger value="posts">
					<BetweenHorizontalEndIcon class="size-4" />
					<span class="ml-2 hidden sm:inline">Posts</span>
				</TabsTrigger>
				<TabsTrigger value="tagged">
					<UsersIcon class="size-4" />
					<span class="ml-2 hidden sm:inline">Tagged</span>
				</TabsTrigger>
			</TabsList>
			<TabsContent value="posts">
				<PhotoGrid />
			</TabsContent>
			<TabsContent value="tagged">
				<div class="flex h-48 items-center justify-center text-muted-foreground">No tagged photos</div>
			</TabsContent>
		</Tabs>
	</div>
</main>
