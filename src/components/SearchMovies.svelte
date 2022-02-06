<script>
	let movie_search = '';
	// Only when the user types something in the search bar, the button shows up.
	let active = false;
	import { goto } from '$app/navigation';
	import { fly } from 'svelte/transition';
	import { circOut } from 'svelte/easing';

	const submitSearch = async (e) => {
		await goto('/searched/' + movie_search);
	};
</script>

<form on:submit|preventDefault={submitSearch} class="search" autocomplete="off">
	<input
		bind:value={movie_search}
		type="text"
		name="search_movies"
		placeholder="Search movie"
		on:focus={() => (active = true)}
		on:blur={() => (active = false)}
	/>
	{#if movie_search}
		<button
			in:fly={{ x: 3.6 * 16, duration: 500, easing: circOut }}
			out:fly={{ x: 3.6 * 16, duration: 500 }}>Search</button
		>
	{/if}
</form>

<style>
	button {
		font-size: 0.8rem;
		padding: 0.5rem 0.5rem;
		background: rgb(255, 130, 130);
		color: white;
		font-weight: bold;
		border: none;
		border-top-right-radius: 0.4rem;
		border-bottom-right-radius: 0.4rem;
		cursor: pointer;
		margin-left: -3.6rem;
	}

	input {
		padding: 0.5rem 0.5rem;
		height: 20%;
		font-weight: bold;
		background-color: rgb(49, 49, 49);
		outline: none;
		border: none;
		color: white;
		border-radius: 0.4rem;
		width: 30%;
	}

	input::placeholder {
		color: rgb(168, 168, 168);
	}
</style>
