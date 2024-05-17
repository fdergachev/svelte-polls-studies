<script>
   import { fade, slide, scale } from "svelte/transition";
   import { flip } from "svelte/animate";
   import PollStore from "../../stores/PollStore.js";
   import PollDetails from "./PollDetails.svelte";
   // export let polls = [];

   // const unsub = PollStore.subscribe((data) => {
   //    polls = data;
   // });

   // onDestroy(() => {
   //    unsub();
   // });
</script>

<div class="poll-list">
   {#each $PollStore as poll (poll.id)}
      <div in:fade|global out:slide animate:flip={{ duration: 300 }}>
         <PollDetails {poll} />
      </div>
   {:else}
      <div>No polls currently exist</div>
   {/each}
</div>

<style>
   .poll-list {
      display: grid;
      grid-template-columns: 1fr 1fr;
      grid-gap: 20px;
   }
</style>
