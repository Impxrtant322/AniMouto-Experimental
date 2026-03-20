<script lang="ts">
  import Button from "$lib/components/Button.svelte";

  export let title: string;
  export let version: string;
  export let items: string[] = [];
  export let onClose: () => void;
</script>

<div class="absolute inset-0 z-50 flex items-center justify-center bg-black/30 backdrop-blur-[2px] p-4">
  <div class="w-full max-w-[380px] overflow-hidden rounded-md border border-white/10 bg-foreground text-text-400 shadow-2xl">
    <div class="h-1 bg-variable"></div>

    <div class="flex items-start justify-between px-4 pt-4 pb-2">
      <div>
        <h2 class="text-[22px] font-semibold leading-none text-text-400">{title}</h2>
        <p class="mt-2 text-sm text-text-200">Version {version}</p>
      </div>

      <button
        type="button"
        aria-label="Close"
        class="flex h-8 w-8 items-center justify-center rounded-md text-[22px] leading-none text-text-200 transition-colors hover:bg-variable/10 hover:text-variable"
        on:click={onClose}
      >
        ×
      </button>
    </div>

    <div class="px-4 pb-4">
      <div class="mt-2 max-h-[220px] overflow-y-auto pr-1">
        <ul class="space-y-3 text-[15px] leading-6 text-text-400">
          {#each items as item}
            <li class="flex items-start gap-3">
              <span class="mt-[1px] shrink-0 text-variable text-sm font-semibold">→</span>
              <span>{item}</span>
            </li>
          {/each}
        </ul>
      </div>

      <div class="mt-5 flex justify-end">
        <Button type="INFO" class="text-sm" on:click={onClose}>
          Got it
        </Button>
      </div>
    </div>
  </div>
</div>