<script>
    import { createEventDispatcher } from 'svelte';
    const dispatch = createEventDispatcher();

    let tabs = ['Create Poll', 'Show Polls'];
    export let currentTab;

    const handleClick = (tab) => {
        currentTab = tab;
        dispatch('changeTab', tab);
    }
</script>

<main>
    <ul>
        <li class:active={currentTab === tabs[0]} on:click={() =>handleClick(tabs[0])}> { tabs[0] } </li>
        <li class:active={currentTab === tabs[1]} on:click={() =>handleClick(tabs[1])}> { tabs[1] } </li>
    </ul>
</main>


<style>
    main {
        margin: 10px 0;
        text-align: center;
    }
    ul {
        margin: 0;
        padding: 0;
        list-style-type: none;
    }
    li {
        display: inline-block;
        margin-left: 15px;
        color: #555;
        font-size: 14px;
        cursor: pointer;
    }
    li.active {
        color: brown;
        border-bottom: 4px solid crimson;
    }

    
</style>