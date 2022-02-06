<script context="module">
	export async function load({ fetch, params }) {
		console.log(params);
		const url = `https://api.themoviedb.org/3/search/movie?api_key=${
			import.meta.env.VITE_API
		}&language=en-US&query=${params.id}&page=1&include_adult=false`;
		const res = await fetch(url);

		const searchedMovies = await res.json();

		if (res.ok) {
			return {
				// No .results here.
				props: { searchedMovies: searchedMovies.results }
			};
		}
	}
</script>

<script>
	export let searchedMovies;
	import MovieCard from '../../components/MovieCard.svelte';
	import { fly } from 'svelte/transition';
	import { onMount } from 'svelte';
	import * as animateScroll from 'svelte-scrollto';
	onMount(() => {
		setTimeout(() => {
			animateScroll.scrollToTop();
		});
	}, 1000);

	// The following uses FormData, excellent if you have multiple key/value pairs to send.
	function searchMovie(e) {
		const formData = new FormData(e.target);
		const search = formData.get('search');
		navigate(`/search/${search}`);
	}
</script>

<div
	class="searched-movies"
	in:fly={{ y: 70, duration: 500, delay: 1000 }}
	out:fly={{ duration: 500 }}
>
	{#each searchedMovies as movie}
		<MovieCard {movie} />
	{/each}
</div>

<style>
	.searched-movies {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
		column-gap: 1rem;
		row-gap: 1rem;
	}
</style>
