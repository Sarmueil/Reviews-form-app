<script>
    import { v4 as uuidv4 } from "uuid";
    import {ReviewStore} from '../store'
    import Button from "./Button.svelte";
    import Card from "./Card.svelte";
    import RatingSelect from "./RatingSelect.svelte";

    let text = "";
    let btnDisabled = true;
    let min = 10;
    let message;
    let rating;


    const handleInputChange = () => {
        if (text.trim().length <= min) {
            message = `you can not input less than ${min} characters`;
            btnDisabled = true;
        } else {
            message = null;
            btnDisabled = false;
        }
    };

    const handleSelect = (e) => (rating = e.detail);

    const handleSubmit = () => {
        if (text.trim().length > min) {
            const newReview = {
                id: uuidv4(),
                text,
                rating: +rating,
            };
           ReviewStore.update((currentReview)=>{
               return [newReview, ...currentReview]
           })
            text=''
        }
    };
</script>

<Card>
    <header>
        <h2>How would you like to rate your service with us?</h2>
    </header>
    <form on:submit|preventDefault={handleSubmit}>
        <RatingSelect on:rating-select={handleSelect} />
        <div class="input-group">
            <input
                type="text"
                placeholder="Tell us something that keeps you coming back"
                bind:value={text}
                on:input={handleInputChange}
            />
            <Button disabled={btnDisabled} type="submit">Send</Button>
        </div>
        {#if message}
            <div class="message">{message}</div>
        {/if}
    </form>
</Card>

<style>
    header {
        max-width: 400px;
        margin: auto;
    }
    header h2 {
        font-size: 16px;
    }
    .input-group {
        display: flex;
        flex-direction: row;
        border: 1px solid #ccc;
        padding: 8px 10px;
        border-radius: 8px;
        margin-top: 15px;
    }

    input {
        flex-grow: 2;
        border: none;
        font-size: 16px;
    }

    input:focus {
        outline: none;
    }
    .message {
        padding-top: 10px;
        text-align: center;
        color: rebeccapurple;
    }
</style>
