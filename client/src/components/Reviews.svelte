<script>
    import {ReviewStore} from '../store';
    // import {onDestroy} from 'svelte'
    import ReviewsCard from "./ReviewsCard.svelte";
    import { fade, scale } from "svelte/transition";
    // export let feedBacks = [];

    //long process

    // const unsubscribe = ReviewStore.subscribe((data)=> feedBacks = data)

    // onDestroy(()=>{
    //     unsubscribe()
    // })

</script>

<main>
    {#each $ReviewStore as feedBack (feedBack.id)}
        <div in:scale out:fade={{duration:500}}>
            <ReviewsCard {feedBack} />
        </div>
    {/each}
</main>
