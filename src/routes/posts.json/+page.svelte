<script>
import { onMount } from "svelte";

// Synthesised meta data from `openAI`
export let data;

let log = console.log; // learn: youtube.com/watch?v=0k4NwimfszA
let posts = [];

// learn: onMount(async () => { posts = await getPosts() });

const getPosts = async() => {
	const response = await fetch("./posts.json");
	// learn: ...huge: youtu.be/xJ0MSOWTnz4?t=131

	const data = await response.json()
	// usage: log(data)
	return data
}

</script>


{#await getPosts()}
	<small class="f8 code">Loading&hellip;</small>
{:then data}
	<!-- usage: {JSON.stringify(data)} -->
	{ JSON.stringify(data, null, 2) }
	{#each data.posts as post }
		{post.id}<br>
		{post.title}<br>
		{post.slug}<br>
		{post.tags}<br>
		{post.date}<br>
		{post.excerpt}<br>
		<code>
			{@html post.content.html}<br>
		</code>
	{/each}
{/await}





<style>
	:global(html, body) { padding:0 }
</style>