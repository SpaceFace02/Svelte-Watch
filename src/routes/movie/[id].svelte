<!-- The empty array signifies dynamism, no matter the url, it will always route here. id is the param. -->
<script context="module">
	export async function load({ fetch, params }) {
		const url = `https://api.themoviedb.org/3/movie/${params.id}?api_key=${
			import.meta.env.VITE_API
		}&language=en-US`;
		const res = await fetch(url);

		const details = await res.json();

		if (res.ok) {
			return {
				// No .results here.
				props: { details }
			};
		}
	}
</script>

<script>
	export let details;
	import { fly } from 'svelte/transition';
	import { onMount } from 'svelte';
	import * as animateScroll from 'svelte-scrollto';
	onMount(() => {
		setTimeout(() => {
			animateScroll.scrollToTop();
		});
	}, 1000);
</script>

<div
	class="movie-details"
	in:fly={{ y: 70, duration: 500, delay: 1000 }}
	out:fly={{ duration: 500 }}
>
	<div class="img-container">
		<img
			src={`https://image.tmdb.org/t/p/original${details.backdrop_path}`}
			alt=""
		/>
	</div>
	<div class="text-container">
		<h1>{details.title}</h1>
		<p class="overview">{details.overview}</p>
		<p><span>Release Date:</span> {details.release_date}</p>
		<p>
			<span>Budget(in million): </span>
			{String(details.budget).slice(0, -6)}
		</p>

		<p><span>Rating: </span> {details.vote_average}</p>

		<p><span>Duration:</span> {details.runtime}</p>
	</div>
</div>

<style>
	.img-container {
		width: 100%;
	}
	img {
		width: 100%;
		border-radius: 0.8rem;
	}
	.movie-details {
		margin: 2rem 10%;
	}
	span {
		font-weight: bold;
	}
</style>
