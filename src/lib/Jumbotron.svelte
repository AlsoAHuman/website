<script lang="ts" context="module">
	import { cubicIn, cubicOut } from 'svelte/easing';
	import { writable } from 'svelte/store';
	import { fly } from 'svelte/transition';

	export const title = writable('');
</script>

<script lang="ts">
	export let img = '/images/jumbotron.png';
</script>

{#if $title}
	<div class="jumbotron" role="banner" style="background-image: url('{img}')">
		<div class="inner">
			{#key $title}
				<h2
					in:fly={{ easing: cubicOut, x: 10, duration: 300, delay: 400 }}
					out:fly={{ easing: cubicIn, x: -10, duration: 300 }}
				>
					{@html $title}
				</h2>
			{/key}
		</div>
	</div>
{/if}

<style>
	.jumbotron {
		background-size: cover;
		background-position: center;
		height: 26rem;
		width: 100%;
		display: flex;
		align-items: center;
		justify-content: center;
	}
	.inner {
		background-color: rgba(0, 0, 0, 0.2);
		width: 100%;
		height: 100%;
		display: flex;
		align-items: center;
	}

	.jumbotron h2 {
		font-family: 'Bebas Neue', sans-serif;
		color: white;
		font-weight: 600;
		line-height: 3.75rem;
		font-size: 4rem;
		max-width: 42.75rem;
		font-style: normal;

		/* position as in prototype, which is not yet finalized. */
		position: relative;
		left: 1.95rem;
	}

	@media screen and (max-width: 500px) {
		.jumbotron h2 {
			margin: 0;
			max-width: 90%;
		}
	}

	@media screen and (max-width: 400px) {
		.jumbotron h2 {
			font-size: 3.5rem;
		}
	}

	@media screen and (max-width: 350px) {
		.jumbotron h2 {
			font-size: 3rem;
			line-height: 3.25rem;
		}
	}
</style>
