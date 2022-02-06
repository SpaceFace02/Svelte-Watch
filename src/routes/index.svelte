<!-- Runs before the components mounts/rendered. -->
<script context="module">
	export async function load({ fetch }) {
		const url = `https://api.themoviedb.org/3/movie/popular?api_key=${
			import.meta.env.VITE_API
		}&language=en-US&page=1`;
		const res = await fetch(url);

		const data = await res.json();

		if (res.ok) {
			return {
				props: {
					// We will alo use search data, so rename it to popular.
					popular: data.results
				}
			};
		}
	}
</script>

<script>
	export let popular;
	import SearchMovies from '../components/SearchMovies.svelte';
	import PopularMovies from '../components/PopularMovies.svelte';
	import { fly } from 'svelte/transition';
</script>

<section in:fly={{ y: 70, duration: 500 }} out:fly={{ duration: 500 }}>
	<SearchMovies />
	<PopularMovies {popular} />
</section>

<!-- This doesn't do SSR, its like react -->

<!-- <script>
    // Whenever the component mounts, fetch data
    import { onMount } from "svelte";
</script> -->
