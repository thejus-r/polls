<script>
    import PollStore from "../stores/PollStore";
    import { createEventDispatcher } from "svelte";
    import Button from "../shared/Button.svelte";

    let dispatch = createEventDispatcher();

    let fields = { question: "", answerA: "", answerB: "" };
    let errors = { question: "", answerA: "", answerB: "" };
    let valid = false;

    const submitHandler = () => {
        valid = true;

        if (fields.question.trim().length < 5) {
            valid = false;
            errors.question = "Question must be atleast 5 char long!";
        } else {
            errors.question = "";
        }

        if (fields.answerA.trim().length < 1) {
            valid = false;
            errors.answerA = "Answer must be atleast 1 Character long!";
        } else {
            errors.answerA = "";
        }

        if (fields.answerB.trim().length < 1) {
            valid = false;
            errors.answerB = "Answer must be atleast 1 Character long!";
        } else {
            errors.answerB = "";
        }

        //add poll
        if (valid) {
            let poll = { ...fields, votesA: 0, votesB: 0, id: Math.random() };
            //save poll to store

            PollStore.update((currentPolls) => {
                return [poll, ...currentPolls];
            });
            dispatch("add");
        }
    };
</script>

<style>
    form {
        width: 400px;
        margin: 0 auto;
        text-align: center;
    }
    .form-field {
        margin: 18px auto;
    }
    input {
        width: 100%;
        border-radius: 6px;
    }
    label {
        margin: 10px auto;
        text-align: left;
    }
    .error {
        color: red;
        font-size: 12px;
        font-weight: bold;
    }
</style>

<form on:submit|preventDefault={submitHandler}>
    <div class="form-field">
        <label for="question">Poll Question</label>
        <input type="text" id="question" bind:value={fields.question} />
        <div class="error">{errors.question}</div>
    </div>
    <div class="form-field">
        <label for="answer-a">Answer A:</label>
        <input type="text" id="answer-a" bind:value={fields.answerA} />
        <div class="error">{errors.answerA}</div>
    </div>
    <div class="form-field">
        <label for="answer-b">Answer B:</label>
        <input type="text" id="answer-b" bind:value={fields.answerB} />
        <div class="error">{errors.answerB}</div>
    </div>
    <Button type="secondary" flat="true">Add Poll</Button>
</form>
