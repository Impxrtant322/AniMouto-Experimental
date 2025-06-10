<script lang="ts">
	import { createEventDispatcher } from "svelte";
	import { fade } from "svelte/transition";
	import { useParams } from "svelte-navigator";
	import { queryStore, getContextClient } from "@urql/svelte";
	import Icon from "svelte-fa";
	import { faTimes } from "@fortawesome/free-solid-svg-icons";
	import {
		GetFullUserMediaListDocument,
		GetMediaByIdDocument,
		MediaListStatus,
		type GetMediaByIdQuery,
	} from "@anilist/graphql";
	import { textify, hexToRgb } from "$lib/util";
	import Button from "$lib/components/Button.svelte";
	import { user } from "$lib/store";

	export let entry: GetMediaByIdQuery["Media"] | null;

	const dispatch = createEventDispatcher();
	const params = useParams();
	const client = getContextClient();

	$: media = queryStore({
		client,
		query: GetMediaByIdDocument,
		variables: {
			id: parseInt($params.id),
		},
	});
	/*
  $: {
    let currentId = entry?.id;
    let name = $user?.name;

    let isIdTruthy = !!currentId;
    let isNameTruthy = !!name;

  console.log('Is ID considered truthy?', isIdTruthy);
  console.log('Is Name considered truthy?', isNameTruthy);

    if (isIdTruthy && isNameTruthy) {
      console.log("Running media search")
      media = queryStore({
        client,
        query: GetFullUserMediaListDocument,
        variables: { userName: name, mediaId: currentId }
      });
    }

    console.log($media)
  }
    */

	// form state
	let status: MediaListStatus | "" = "";
	let score = 0;
	let progress = 0;
	let startDate = "";
	let finishDate = "";
	let rewatchCount = 0;
	let notes = "";

	/*
  if($media.data?.MediaList) {
    status = $media.data.MediaList.status || null;
    score = $media.data.MediaList.score || 0;
    progress = $media.data.MediaList.progress || 0;
    startDate = ""
    finishDate = ""
    rewatchCount = $media.data.MediaList.repeat || 0;
    notes = $media.data.MediaList.notes || "";
  }
    */

	function close() {
		dispatch("close");
	}
	function save() {
		close();
	}
</script>

<div class="fixed inset-0 z-20 flex items-center justify-center bg-background">
	<div
		class="absolute inset-0 backdrop-blur-[10px] bg-background/40"
		on:click={close}
	/>

	<div
		class="relative w-full max-w-5xl mx-4
           bg-surface dark:bg-background
           rounded-2xl shadow-2xl overflow-hidden"
		in:fade={{ duration: 200 }}
	>
		<div
			class="relative w-full {$media.data.Media.bannerImage
				? 'h-[20vh]'
				: 'h-[24vh] -mt-[4vh]'} bg-cover bg-center"
			style="background-image:url({$media.data.Media.bannerImage ||
				$media.data.Media.coverImage.extraLarge})"
		>
			<div class="h-full w-full bg-gradient-to-b from-shadow/40 to-shadow/60" />

			<div
				class="absolute left-6 bottom-4 transform translate-y-1/2 flex items-end space-x-4"
			>
				<img
					src={$media.data.Media.coverImage.medium}
					alt="{$media.data.Media.title.userPreferred} poster"
					class="w-24 sm:w-32 rounded-xl shadow-lg border-2 border-white"
				/>
				<div class="text-text drop-shadow-md">
					<h2 class="text-xl sm:text-2xl font-bold leading-tight">
						{$media.data.Media.title.userPreferred}
					</h2>
					<p class="text-sm sm:text-base text-text-secondary">
						{$media.data.Media.format} • {$media.data.Media.status}
					</p>
				</div>
			</div>
			<button
				class="absolute top-4 right-4 p-2 text-white"
				on:click={close}
				aria-label="Close editor"
			>
				<Icon icon={faTimes} />
			</button>
		</div>

		<div
			class="w-full mt-16 px-6 pb-6 relative z-10"
			style="--color-variable:{hexToRgb($media.data.Media.coverImage.color) ||
				'var(--color-accent)'}"
		>
			<div class="grid grid-cols-3 gap-2">
				<div>
					<label class="block text-sm text-text-secondary mb-1">Status</label>
					<select
						bind:value={status}
						class="w-full px-3 py-2 bg-surface dark:bg-background border rounded text-text focus:ring-2 focus:ring-variable"
					>
						{#if !status}
							<option value="" disabled>Status</option>
						{/if}
						{#each Object.values(MediaListStatus) as s}
							{#if s == "CURRENT"}
								<option value={s}>Watching</option>
							{:else if s == "PLANNING"}
								<option value={s}>Plan to watch</option>
							{:else if s == "COMPLETED"}
								<option value={s}>Completed</option>
							{:else if s == "REPEATING"}
								<option value={s}>Rewatching</option>
							{:else if s == "PAUSED"}
								<option value={s}>Paused</option>
							{:else if s == "DROPPED"}
								<option value={s}>Dropped</option>
							{:else}
								<option value={s}>{textify(s)}</option>
							{/if}
						{/each}
					</select>
				</div>

				<div>
					<label class="block text-sm text-text-secondary mb-1">Score</label>
					<input
						type="number"
						min="0"
						max="100"
						bind:value={score}
						class="w-full px-3 py-2 bg-surface dark:bg-background border rounded text-text focus:ring-2 focus:ring-variable"
					/>
				</div>

				<div>
					<label class="block text-sm text-text-secondary mb-1"
						>Episode Progress</label
					>
					<input
						type="number"
						min="0"
						bind:value={progress}
						class="w-full px-3 py-2 bg-surface dark:bg-background border rounded text-text focus:ring-2 focus:ring-variable"
					/>
				</div>

				<div>
					<label class="block text-sm text-text-secondary mb-1"
						>Start Date</label
					>
					<input
						type="date"
						bind:value={startDate}
						class="w-full px-3 py-2 bg-surface dark:bg-background border rounded text-text focus:ring-2 focus:ring-variable"
					/>
				</div>
				<div>
					<label class="block text-sm text-text-secondary mb-1"
						>Finish Date</label
					>
					<input
						type="date"
						bind:value={finishDate}
						class="w-full px-3 py-2 bg-surface dark:bg-background border rounded text-text focus:ring-2 focus:ring-variable"
					/>
				</div>

				<div>
					<label class="block text-sm text-text-secondary mb-1"
						>Total Rewatches</label
					>
					<input
						type="number"
						min="0"
						bind:value={rewatchCount}
						class="w-full px-3 py-2 bg-surface dark:bg-background border rounded text-text focus:ring-2 focus:ring-variable"
					/>
				</div>
			</div>
			<div class="mt-4">
				<label class="block text-sm text-text-secondary mb-1">Notes</label>
				<textarea
					rows="3"
					bind:value={notes}
					class="w-full px-3 py-2 bg-surface dark:bg-background border rounded text-text resize-none focus:ring-2 focus:ring-variable"
					placeholder="Type your notes…"
				/>
			</div>
			<div class="mt-6 flex justify-end space-x-2">
				<Button type="INFO" on:click={save}>Save</Button>
				<Button type="ERROR" on:click={close}>Cancel</Button>
			</div>
		</div>
	</div>
</div>
