<script>
   import Container from "./lib/general/Container.svelte";
   import Header from "./lib/components/Header.svelte";
   import Footer from "./lib/components/Footer.svelte";
   import Tabs from "./lib/general/Tabs.svelte";
   import CreatePollForm from "./lib/components/CreatePollForm.svelte";
   import PollList from "./lib/components/PollList.svelte";

   //tabs
   let items = ["Current Polls", "Create Poll"];
   let activeItem = "Current Polls";
   function tabChange(e) {
      activeItem = e.detail;
   }

   //polls

   function handleAdd(e) {
      activeItem = "Current Polls";
   }

   // handle votes
</script>

<Header />
<main>
   <Container>
      <div class="mt-[40px]">
         <Tabs {items} {activeItem} on:tabChange={tabChange} />
         {#if activeItem === "Current Polls"}
            <PollList />
         {:else if activeItem === "Create Poll"}
            <CreatePollForm on:addPoll={handleAdd} />
         {/if}
      </div>
   </Container>
</main>
<Footer />

<style>
</style>
