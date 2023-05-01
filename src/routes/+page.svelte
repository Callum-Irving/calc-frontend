<script lang="ts">
	const backend_url = 'https://subtle-sundae-f6dc84.netlify.app/.netlify/functions/calc';
	let input = '';
	let results = '';
	async function evalStmts() {
		let response = await fetch(backend_url, {
			method: 'POST',
			body: JSON.stringify({
				stmts: input
			})
		});

		console.log(response);

		let res = await response.json();
		if ('results' in res) {
			results = res.results;
		} else {
			results = 'ERROR';
		}
	}
</script>

<h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>
<textarea bind:value={input} />
<button on:click={evalStmts}>Run</button>
<p>{results}</p>
