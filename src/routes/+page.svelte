<script lang="ts">
	import '../app.postcss';
	import floria from '$lib/floria.jpg';
	import { fade, scale } from 'svelte/transition';
	import { browser } from '$app/environment';
	import IconBomb from './IconBomb.svelte';
	import { randelt } from './foobar';

	let unclickable: HTMLButtonElement;

	const emojis = [
		'twemoji:rolling-on-the-floor-laughing',
		'fluent-emoji:rolling-on-the-floor-laughing',
		'noto-v1:rolling-on-the-floor-laughing'
	];

	function nop() {
		const e = unclickable;

		const vpw = window.innerWidth;
		const vph = window.innerHeight;

		const ew = e.offsetWidth;
		const eh = e.offsetHeight;

		const mx = vpw - ew;
		const my = vph - eh;

		const rx = Math.floor(Math.random() * mx);
		const ry = Math.floor(Math.random() * my);

		e.style.position = 'fixed';
		e.style.left = `${rx}px`;
		e.style.top = `${ry}px`;
	}

	let emojiTime = false;
	const duration = 2000;

	function falsaa() {
		emojiTime = true;

		setTimeout(() => {
			emojiTime = false;
		}, duration);
	}

	if (browser) {
		window.addEventListener('resize', nop);
	}
</script>

<div class="hero min-h-screen bg-base-200">
	<div class="hero-content text-center">
		<div class="max-w-md flex flex-col gap-2 items-center">
			<h1 class="text-3xl font-bold">Esta mujer es falsa?</h1>
			<img alt="floria" class="rounded-md w-48" src={floria} />
			<div class="flex font-bold gap-3">
				<button in:fade on:click={falsaa} class="btn btn-circle btn-primary">Si</button>
				<button
					in:fade
					bind:this={unclickable}
					on:mouseenter={nop}
					on:click={nop}
					tabindex="-1"
					class="btn btn-secondary">No</button
				>
			</div>
		</div>
	</div>

	{#if emojiTime}
		<div out:scale>
			<IconBomb icon={randelt(emojis)} />
		</div>
	{/if}
</div>

<style>
	button {
		transition-property: left, top;
		transition-duration: 300ms;
	}
</style>
