<script>
    import { createEventDispatcher } from 'svelte';
    const dispatch = createEventDispatcher();
   
    let pollQuestion;
    let optionA;
    let optionB;
    let voteA= 0;
    let voteB= 0;

    let poll = {};

    function createPollHandler() {
        poll = {id:  Math.floor(Math.random()*100), q: pollQuestion, optionA, optionB, voteA, voteB};
        dispatch('addpoll', poll);
        dispatch('changeTab', 'Show Polls');
    }

</script>

<main>
    <div class="create-poll">
        <h3>Create Poll</h3>
        <div class="qna-grid">
            <span>Que: </span> <input type="text" bind:value={pollQuestion}/>
        </div>
        <div>
            <div class="qna-grid">
                <span>Option: A</span> <input type="text" class="option-input" on:input={(e)=> optionA = e.target.value}/>
            </div>
            <div class="qna-grid">
                <span>Option: B</span> <input type="text" class="option-input" on:input={(e)=> optionB = e.target.value}/>
            </div>
        </div>
        <button class="btn btn-primary" on:click={createPollHandler}>Create Poll</button>
    </div>
</main>


<style>
    main {
        padding: 10px;
        background-color: #efefef;
       
    }
    .create-poll {
        max-width: 400px;
        margin: 20px auto;
        padding: 20px;
        background: #fff;
        box-shadow: 1px 1px 2px rgba(0,0,0, .5);
    }
    input {
        display: block;
        width: 100%;
    }
    input.option-input {
        display: inline-block!important;
        width: auto;

    }
    .qna-grid {
        display: grid;
        grid-template-columns: 80px auto;
    }
    .btn {
        display: inline-block;
        font-weight: 400;
        line-height: 1.5;
        color: #212529;
        text-align: center;
        text-decoration: none;
        vertical-align: middle;
        cursor: pointer;
        -webkit-user-select: none;
        -moz-user-select: none;
        user-select: none;
        background-color: transparent;
        border: 1px solid transparent;
        padding: 0.280rem 0.55rem;
        font-size: 1rem;
        border-radius: 0.25rem;
        transition: color .15s ease-in-out,background-color .15s ease-in-out,border-color .15s ease-in-out,box-shadow .15s ease-in-out;
    } 
    .btn-primary {
        color: #fff;
        background-color: #0d6efd;
        border-color: #0d6efd;
    }
    
</style>