<script>
  import ListItem from "./ListItem.svelte";
  export let events;
  export let toggleModal;
  export let deleteEvent;
</script>

<div class="grid-cols-1 lg:grid-cols-2 grid gap-4">
  {#if events && events.length}
    {#each events as event}<ListItem {...event} deleteEvent={deleteEvent} />{/each}
  {:else}
    <p class="text-center">Get started by adding your first event:</p>
    <button
      on:click={toggleModal}
      type="button"
      class="text-white bg-blue-500 hover:bg-blue-800 font-medium rounded-lg text-sm px-5 py-2 mx-auto"
      >Add an Event</button
    >
  {/if}
</div>
