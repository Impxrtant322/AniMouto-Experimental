<script lang="ts">
  import { Link } from "svelte-navigator";
  import NotificationContainer from "./NotificationContainer.svelte";

  type SubmissionSubject = {
    id: number,
    name?: { full: string },
    title?: { userPreferred: string },
    img?: { large: string, color?: string },
    url?: string,
  };

  export let notification: {
    createdAt: number,
    type: string,
    status?: string,
    notes?: string,
    submittedTitle?: string,
    media?: SubmissionSubject,
    staff?: SubmissionSubject,
    character?: SubmissionSubject,
  };
  export let unread = false;

  $: subject = notification.media ?? notification.staff ?? notification.character;
  $: name = notification.media?.title?.userPreferred ?? subject?.name?.full ?? notification.submittedTitle ?? "your submission";
  $: status = (notification.status ?? "updated").toLowerCase();
</script>

<NotificationContainer {unread} createdAt={notification.createdAt}>
  {#if subject?.img?.large}
    <img src={subject.img.large} alt="Key visual" class="w-12 mr-4 object-center object-cover aspect-[3/4]" />
  {/if}
  <span class="line-clamp-3 mr-6 flex-1">
    Your submission for
    {#if notification.media}
      <Link to="/media/{notification.media.id}" class="font-medium hover:text-accent transition-colors">{name}</Link>
    {:else if subject?.url}
      <a href={subject.url} target="_blank" class="font-medium hover:text-accent transition-colors">{name}</a>
    {:else}
      <span class="font-medium">{name}</span>
    {/if}
    was {status}.
    {#if notification.notes}
      <span class="italic">{notification.notes}</span>
    {/if}
  </span>
</NotificationContainer>