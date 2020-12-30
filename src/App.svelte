<script>
import CreatePollForm from "./components/CreatePollForm.svelte";
import Footer from "./components/Footer.svelte";
import Header from "./components/Header.svelte";
import Tabs from "./shared/Tabs.svelte";

// tabs 

let items = ['Current Polls','Add New Poll'];
let activeItem = 'Current Polls';

const tabChange = (e) => {
	activeItem = e.detail;
}

</script>

<Header/>

<main>
	<Tabs {activeItem} {items} on:tabChange={tabChange}/>
	{#if activeItem === "Add New Poll"}
		<CreatePollForm/>
	{:else if activeItem === "Current Polls"}
		<p>Current Pools</p>
	{/if}
</main>


<Footer/>

<style>
	main{
		max-width: 960px;
		margin: 40px auto;
	}
</style>