<script>
	import CreatePollForm from "./components/CreatePollForm.svelte";
	import Footer from "./components/Footer.svelte";
	import Header from "./components/Header.svelte";
	import PollList from "./components/PollList.svelte";
	import Tabs from "./shared/Tabs.svelte";

	// tabs

	let items = ["Current Polls", "Add New Poll"];
	let activeItem = "Current Polls";

	const tabChange = (e) => {
		activeItem = e.detail;
	};

	const handleAdd = (e) => {
		activeItem = "Current Polls";
	};
</script>

<style>
	main {
		max-width: 960px;
		margin: 40px auto;
	}
</style>

<Header />

<main>
	<Tabs {activeItem} {items} on:tabChange={tabChange} />
	{#if activeItem === 'Add New Poll'}
		<CreatePollForm on:add={handleAdd} />
	{:else if activeItem === 'Current Polls'}
		<PollList />
	{/if}
</main>

<Footer />
