<script lang="ts">
	import { Link } from "svelte-navigator";
	import {
		NotificationType,
		type MediaFragment,
		type AiringNotification,
		type RelatedMediaAdditionNotification,
		type MediaDataChangeNotification,
	} from "@anilist/graphql";
	import { hexToRgb } from "$lib/util";
	import NotificationContainer from "./NotificationContainer.svelte";

	export let notification: Pick<
		| AiringNotification
		| RelatedMediaAdditionNotification
		| MediaDataChangeNotification,
		"createdAt" | "type"
	> & {
		context?: string;
		contexts?: string[];
		episode?: number;
		media: Pick<MediaFragment, "id" | "title" | "img">;
	};
	export let unread = false;

	let frozenId: number | null = null;
	$: if (notification?.media && frozenId === null) {
		frozenId = notification.media.id;
	}
</script>

<NotificationContainer {unread} createdAt={notification.createdAt}>
	{#if frozenId !== null}
		<Link to={`/media/${frozenId}`} class="flex-none">
			<img
				src={notification.media.img?.large || "/placeholder.png"}
				alt={notification.media.title?.userPreferred || "Media"}
				class="w-12 mr-4 object-center object-cover aspect-[3/4]"
			/>
		</Link>

		<Link
			to={`/media/${frozenId}`}
			class="line-clamp-3 mr-6 flex-1"
			style="--color-variable: {hexToRgb(notification.media.img?.color) ||
				'var(--color-accent)'}"
		>
			{#if notification.type === NotificationType.AIRING}
				{notification.contexts?.[0] || ""}
				{notification.episode ?? ""}
				{notification.contexts?.[1] || ""}
				<span class="font-medium hover:text-variable transition-colors">
					{notification.media.title?.userPreferred || "Unknown Title"}
				</span>
				{notification.contexts?.[2] || ""}
			{:else}
				<span class="font-medium hover:text-variable transition-colors">
					{notification.media.title?.userPreferred || "Unknown Title"}
				</span>
				{notification.context || ""}
			{/if}
		</Link>
	{:else}
		<div class="flex items-center space-x-4 opacity-50 cursor-not-allowed">
			<div class="w-12 h-16 bg-gray-200 rounded-md"></div>

			<div class="flex-1 space-y-1">
				<div class="h-4 bg-gray-200 rounded w-3/4"></div>
				<div class="h-3 bg-gray-200 rounded w-1/2"></div>
			</div>
		</div>
	{/if}
</NotificationContainer>
