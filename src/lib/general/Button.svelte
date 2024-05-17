<script>
   export let type = "primary";
   export let flat = false;
   export let inverse = false;
</script>

<button class={type} class:flat class:inverse on:click>
   <slot></slot>
</button>

<style>
   button {
      border: none;
      border-radius: 6px;
      padding: 8px 12px;
      cursor: pointer;
      font-weight: bold;
      box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.2);
      transition: all 0.2s ease-in-out;
   }
   button:hover.inverse.primary {
      background-color: #ffe7df;
   }
   button:hover.inverse.secondary {
      background-color: #96d2bc;
   }
   button:hover.primary {
      background-color: #af2900;
   }
   .primary {
      background-color: #ff3d00;
      color: white;
   }

   .secondary {
      background-color: #45c496;
      color: #fff;
   }
   .flat {
      box-shadow: none;
   }
   button:hover.secondary {
      background-color: #2d8665;
   }
   .inverse.primary {
      background-color: white;
      color: #ff3d00;
      border: 2px solid #ff3d00;
   }
   .inverse.secondary {
      background-color: #f7f7f7;
      color: #45c496;
      border: 2px solid #45c496;
   }
</style>
