<script>
   import PollStore from "../../stores/PollStore";
   import Card from "../general/Card.svelte";
   import Button from "../general/Button.svelte";
   export let poll;

   //reactive value
   $: totalVotes = poll.votesA + poll.votesB;
   $: percentA = Math.floor((poll.votesA / totalVotes) * 100);
   $: percentB = Math.floor((poll.votesB / totalVotes) * 100);

   //handling votes
   function handleVote(option, id) {
      PollStore.update((polls) => {
         let copiedPolls = [...polls];
         let upvotedPoll = copiedPolls.find((poll) => poll.id == id);
         if (option === "a") {
            upvotedPoll.votesA++;
         } else {
            upvotedPoll.votesB++;
         }
         return copiedPolls;
      });
   }
   function handleClick(id) {
      PollStore.update((polls) => {
         return polls.filter((poll) => poll.id !== id);
      });
   }
</script>

<Card>
   <div class="poll">
      <h3>{poll.question}</h3>
      <p>Total votes: {totalVotes}</p>
      <div class="answer" on:click={() => handleVote("a", poll.id)}>
         <div class="percent percent-a" style="width: {percentA}%;"></div>
         <span>{poll.answerA} ({poll.votesA})</span>
      </div>
      <div class="answer" on:click={() => handleVote("b", poll.id)}>
         <div class="percent percent-b" style="width: {percentB}%;"></div>
         <span>{poll.answerB} ({poll.votesB})</span>
      </div>
      <div class="text-center mt-[20px]">
         <Button flat={true} on:click={() => handleClick(poll.id)}
            >Delete</Button
         >
      </div>
   </div>
</Card>

<style>
   h3 {
      margin: 0 auto;
      color: #555;
      font-size: 20px;
      font-weight: bold;
   }
   p {
      margin-top: 6px;
      font-size: 14px;
      color: #aaa;
      margin-bottom: 30px;
   }
   .answer {
      cursor: pointer;
      background: #fafafa;
      margin: 10px auto;
      position: relative;
      transition: all 0.15s ease-in-out;
   }
   .answer:hover {
      opacity: 0.6;
   }
   span {
      display: inline-block;
      padding: 10px 20px;
      font-size: 16px;
   }
   .percent {
      height: 100%;
      position: absolute;
      box-sizing: border-box;
   }
   .percent-a {
      border-left: 4px solid #ff3d00;
      background: rgba(217, 27, 66, 0.2);
   }
   .percent-b {
      border-left: 4px solid #45c496;
      background: rgba(69, 196, 150, 0.2);
   }
</style>
