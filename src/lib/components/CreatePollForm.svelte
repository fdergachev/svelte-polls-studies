<script>
   import PollStore from "../../stores/PollStore.js";
   import Button from "../general/Button.svelte";
   import { createEventDispatcher } from "svelte";
   const dispatch = createEventDispatcher();

   let fields = { question: "", answerA: "", answerB: "" };
   let errors = { question: "", answerA: "", answerB: "" };
   let valid = false;

   function submitHandler() {
      valid = true;
      //validate question
      if (fields.question.trim().length < 5) {
         errors.question = "Question must be at least 5 characters long";
         valid = false;
      } else {
         errors.question = "";
      }

      //validate answer A
      if (fields.answerA.trim().length < 1) {
         errors.answerA = "Answer A is required";
         valid = false;
      } else {
         errors.answerA = "";
      }

      //validate answer B
      if (fields.answerB.trim().length < 1) {
         errors.answerB = "Answer B is required";
         valid = false;
      } else {
         errors.answerB = "";
      }

      //add new poll
      if (valid) {
         const poll = { ...fields, votesA: 0, votesB: 0, id: Math.random() };
         //save poll to store
         PollStore.update((currentPolls) => {
            return [poll, ...currentPolls];
         });
         dispatch("addPoll");
      }
   }
</script>

<form on:submit|preventDefault={submitHandler}>
   <div class="form-filed">
      <label for="question">Poll Question:</label>
      <input type="text" id="question" bind:value={fields.question} />
      <div class="error">{errors.question}</div>
   </div>
   <div class="form-filed">
      <label for="answer-a">Answer A:</label>
      <input type="text" id="answer-a" bind:value={fields.answerA} />
      <div class="error">{errors.answerA}</div>
   </div>
   <div class="form-filed">
      <label for="answer-b">Answer B:</label>
      <input type="text" id="answer-b" bind:value={fields.answerB} />
      <div class="error">{errors.answerB}</div>
   </div>
   <Button type="secondary" flat={true}>Add Poll</Button>
</form>

<style>
   form {
      width: 400px;
      margin: 0 auto;
      text-align: center;
   }
   .form-filed {
      margin: 20px 0;
   }
   input {
      width: 100%;
      border-radius: 6px;
      background-color: #f7f7f7;
      padding: 10px 15px;
      outline: 1px solid #f7f7f7;
      transition: all 0.2s ease-in-out;
      margin: 10px 0;
   }
   input:focus {
      outline: 1px solid #ccc;
   }
   label {
      display: block;
      text-align: left;
   }
   .error {
      color: #ff3d00;
      font-weight: bold;
      font-size: 12px;
   }
</style>
