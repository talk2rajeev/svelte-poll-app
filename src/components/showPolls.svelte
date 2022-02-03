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
    .card {
        padding: 20px;
        background: #fff;
        box-shadow: 1px 1px 2px rgba(0,0,0, .5);
    }
    .card > h4 {
        margin: 0;
        padding: 0;
        margin-bottom: 20px;
    }
    .percent-wrapper{
        margin-bottom: 15px;
        background: #eeebeb;
        line-height: 1.5em;
        position: relative;
        border: 1px solid transparent;
    }
    .percent-wrapper:hover {
        opacity: .5;
        border: 1px solid #ddd;
        cursor: pointer;
    }
    .percent-wrapper .percent {
        position: absolute;
        top: 0;
        left: 0;
        display: inline-block;
        height: 100%;
        background: rgba(220, 20, 60, .5);
    }
</style>