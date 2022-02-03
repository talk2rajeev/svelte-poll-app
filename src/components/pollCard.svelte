<script>
    import { createEventDispatcher } from 'svelte';
    import { tweened } from 'svelte/motion';
    import { fade, slide, scale } from 'svelte/transition';

    const dispatch = createEventDispatcher();
   
    export let poll;

    function upvote(option) {
        let p = {...poll};

        if(option === 'optionA') {
            p.voteA+=1;
        }
        if(option === 'optionB') {
            p.voteB+=1;
        }
        dispatch('upvote', p)
    }

    function deletePoll() {
        dispatch('deletePoll', poll)
    }

    $: total = poll.voteA + poll.voteB;
    $: percentA = poll.voteA/total * 100 || 0;
    $: percentB = poll.voteB/total * 100 || 0;

    const tweenedA = tweened(0);
    const tweenedB = tweened(0);

    $: tweenedA.set(Math.floor(percentA));
    $: tweenedB.set(Math.floor(percentB));

    Math.floor(percentA)

    $: {
        console.log('total : ', total);
        console.log('percentA : ', tweenedA);
        console.log('percentB : ', tweenedB);
    }

</script>

<div class="card" in:fade out:scale|local>
    <p>{poll.q} ({total})  </p>
    <div>
        <div class="percent-wrapper" on:click={()=>upvote('optionA')} >{poll.optionA}: {poll.voteA} <div class="percent" style="width: {$tweenedA}%;" /> </div>
        <div class="percent-wrapper" on:click={()=>upvote('optionB')} >{poll.optionB}: {poll.voteB} <div class="percent" style="width: {$tweenedB}%;" /> </div>
    </div>
    <div>
        <button on:click={deletePoll}>Delete</button>
    </div>
</div>


<style>
    
    .card {
        padding: 20px;
        background: #fff;
        box-shadow: 1px 1px 2px rgba(0,0,0, .5);
    }
    .card > p {
        margin: 0;
        padding: 0;
        margin-bottom: 20px;
        font-size: 16px;
        font-weight: 500;
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