<script>
	export let movie;
</script>

<div class="movie-card">
	<a sveltekit:noscroll href={`/movie/${movie.id}`}>
		<img
			src={`https://image.tmdb.org/t/p/w500` + movie.poster_path}
			alt={movie.title}
		/>
	</a>

	<div class="description">
		<h2>{movie.title}</h2>
		<p>{movie.release_date}</p>
	</div>
</div>

<!-- Scoped to this file only. -->
<style>
	img {
		width: 100%;
		height: 60vh;
		object-fit: cover;
		border-radius: 0.7rem;
		margin-bottom: 1rem;
	}

	.description {
		width: 100%;
	}
	p {
		font-size: 0.8rem;
		width: 100%;
	}
	h2 {
		font-size: 1.1rem;
		/* align-items: center; */
	}

	.movie-card {
		display: flex;
		flex-direction: column;
	}
</style>
