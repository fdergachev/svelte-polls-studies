<script>
   import { createEventDispatcher } from "svelte";
   const dispatch = createEventDispatcher();

   export let items;
   export let activeItem;
</script>

<div class="tabs mb-10">
   <ul class="flex justify-center p-0">
      {#each items as item}
         <li
            class="mx-[16px] text-[18px] text-[#555] cursor-pointer"
            on:click={() => dispatch("tabChange", item)}
         >
            <div class:active={item === activeItem}>
               {item}
            </div>
         </li>
      {/each}
   </ul>
</div>

<style>
   .active {
      color: #ff3d00;
      font-weight: bold;
      border-bottom: 2px solid #ff3d00;
      padding-bottom: 8px;
   }
</style>
