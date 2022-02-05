<script>
    import PollCard from "./pollCard.svelte";
    import { createEventDispatcher } from 'svelte';

    const dispatch = createEventDispatcher();
   
    export let polls;

    function upvote(e) {
        console.log(e.detail)
        dispatch('upvote', e.detail)
    }

    function deletePoll(e) {
        dispatch('deletePoll', e.detail);
    }

</script>

<div class="main">
    <div class="polls" >
        {#each polls as poll}
            <PollCard poll={poll} on:upvote = {upvote} on:deletePoll={deletePoll}/>
        {/each}
    </div>
</div>


<style>
    .main {
        padding: 20px;
        background-color: #ddd;
    }
    .polls {
        display: grid;
        grid-template-columns: 1fr 1fr;
        grid-gap: 20px;
    }
</style>