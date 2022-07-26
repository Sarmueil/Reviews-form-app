<script>
    import {ReviewStore} from '../store'
    $: count = $ReviewStore.length;
	$: average = Math.trunc(
		$ReviewStore.reduce((a, { rating }) => a + rating, 0) / $ReviewStore.length 
	);

</script>

<div class="feedback_stats">
 <h4>{count} Reviews</h4>
 <h4>Ratings average: {average}</h4>
</div>

<style>
    .feedback_stats {
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
</style>