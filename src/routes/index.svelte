<!-- Basic API request -->
<script context="module">
	export async function load({ fetch }) {
		const res = await fetch(
			`https://api.themoviedb.org/3/movie/popular?api_key=${
				import.meta.env.VITE_API
			}&language=en-US&page=1`
		);
		const data = await res.json();
		if (res.ok) {
			return {
				props: { popular: data.results }
			};
		}
		return {
			props: { popular: 'NONE' }
		};
	}
</script>

<script>
	import PopularMovies from '../components/popularMovies.svelte';
	import SearchMovies from '../components/searchMovies.svelte';
	export let popular;
	import global from '../global.css';
	import { fly } from 'svelte/transition';
</script>

<section in:fly={{ y: 50, duration: 500, delay: 500 }} out:fly={{ duration: 500 }}>
	<SearchMovies />
	<PopularMovies {popular} />
</section>
