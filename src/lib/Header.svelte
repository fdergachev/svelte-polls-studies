<script>
   import svelteLogo from "../assets/svelte.svg";
</script>

<header>
   <div>
      <img src={svelteLogo} alt="Svelte logo" />
      <p>My first svelte powered app</p>
   </div>
</header>

<style>
   header {
      background-color: #f7f7f7;
      padding: 20px;
   }
   div {
      margin: 0;
      display: flex;
      gap: 20px;
      align-items: center;
      text-transform: uppercase;
      letter-spacing: 3px;
      color: rgb(155, 155, 155);
   }
</style>
