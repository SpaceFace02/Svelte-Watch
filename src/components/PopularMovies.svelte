<script>
	export let popular;
	import MovieCard from './MovieCard.svelte';
</script>

<h2>Popular Movies</h2>

<div class="popular-movies">
	{#each popular as movie}
		<MovieCard {movie} />
	{/each}
</div>

<style>
	.popular-movies {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
		column-gap: 1rem;
		row-gap: 1rem;
	}
	h2 {
		margin-bottom: 3rem;
	}
</style>
