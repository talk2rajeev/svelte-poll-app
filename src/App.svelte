<script>
	import  Header   from "./components/Header.svelte";
	import  Footer   from "./components/footer.svelte";
	import  Tabs   from "./components/tabs.svelte";
	import  CreatePoll   from "./components/createPoll.svelte";
	import ShowPolls from './components/showPolls.svelte';

	let currentTab = 'Create Poll';

	let polls = [];

	function addPollHandler(e){
		polls = [...polls, e.detail]
	}
	function changeTab(e) {
		currentTab = e.detail;
	}
	function upvote(e) {
		const poll = e.detail;

		polls = polls.map(p=>p.id === poll.id ? poll : p)
	}
	function deletePoll(e) {
		polls = polls.filter(p => p.id !== e.detail.id);
	}
</script>

<main>
	<Header />
	<div>
		<Tabs currentTab={currentTab} on:changeTab={changeTab}/>
	</div>
	
	<div>
		{#if currentTab === 'Create Poll'}
			<CreatePoll on:addpoll={addPollHandler} on:changeTab={changeTab}/>
		{:else}
			<ShowPolls polls={polls} on:upvote={upvote} on:deletePoll={deletePoll} />	
		{/if}
	</div>
	<Footer />
	
</main>

<style>
	main {
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>