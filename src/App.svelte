<script lang="ts">
  import { Styles } from 'sveltestrap';
	
	let input: string;
	let response: any;
	
	function updateResponse() {
		fetch("https://godsusersearch.dallas.workers.dev?username=" + input)
		.then(response => response.json())
		.then(data => {
			response = data;
		})
		.catch(error => {
			response = error;
		});
	}
</script>

<Styles />

<main>
<input bind:value={input} on:input={updateResponse} placeholder="Enter username..." />

{#if response && response.length > 0}
	<p>Results: ({response.length})</p>
	{#each response as doc}
		<div>
			<h1>{doc.username}</h1>
			<p>user_id: {doc.user_id}</p>
			<p>lost_matches: {doc.lost_matches}</p>
			<p>total_xp: {doc.total_xp}</p>
			<p>won_matches: {doc.won_matches}</p>
			<p>xp_level: {doc.xp_level}</p>
			<p>xp_to_next: {doc.xp_to_next}</p>
		</div>
	{/each}
{:else}
<p>Results: (0)</p>
{/if}
</main>
