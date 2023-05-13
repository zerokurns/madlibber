<script lang="ts">
	import { writable } from 'svelte/store';
	import { faker } from '@faker-js/faker';
	import logo from '$lib/madlibber.png';

	const word = writable('Generate...');

	const setWord = (newWord: string) => {
		$word = newWord;
	};

	const getPlace = () => {
		const randInt = Math.floor(Math.random() * 3) + 1;
		let place: string = '';
		switch (randInt) {
			case 1:
				place = faker.location.city();
			case 2:
				place = faker.location.state();
			case 3:
				place = faker.location.country();
		}
		return place;
	};
</script>

<div class="container h-full mx-auto flex justify-center items-center">
	<div class="space-y-10 text-center flex flex-col items-center">
		<p class="text-4xl font-bold">MadLibber</p>
		<!-- Animated Logo -->
		<figure>
			<img src={logo} alt="madlibber" />
			<div class="img-bg" />
		</figure>
		<!-- / -->
		<div class="flex justify-center space-x-2">
			<div class="card p-6 min-w-[350px]">
				<p class="text-xl font-semibold">{$word}</p>
			</div>
		</div>
		<div class="flex flex-wrap flex-row gap-2 justify-center">
			<button
				class="btn variant-filled"
				type="button"
				on:click|preventDefault={() => {
					setWord(faker.word.adjective());
				}}>Adjective</button
			>
			<button
				class="btn variant-filled"
				type="button"
				on:click|preventDefault={() => {
					setWord(faker.word.adverb());
				}}>Adverb</button
			>
			<button
				class="btn variant-filled"
				type="button"
				on:click|preventDefault={() => {
					setWord(faker.word.noun());
				}}>Noun</button
			>
			<button
				class="btn variant-filled"
				type="button"
				on:click|preventDefault={() => {
					setWord(faker.word.verb());
				}}>Verb</button
			>
			<button
				class="btn variant-filled"
				type="button"
				on:click|preventDefault={() => {
					setWord(getPlace());
				}}>Place</button
			>
			<button
				class="btn variant-filled"
				type="button"
				on:click|preventDefault={() => {
					setWord(faker.person.firstName());
				}}>Name</button
			>
		</div>
		<div class="flex flex-wrap flex-row gap-2 justify-center">
			<button
				class="chip !bg-transparent"
				type="button"
				on:click|preventDefault={() => {
					setWord(faker.animal.type());
				}}>Animal</button
			>
			<button
				class="chip !bg-transparent"
				type="button"
				on:click|preventDefault={() => {
					setWord(faker.color.human());
				}}>Color</button
			>
			<button
				class="chip !bg-transparent"
				type="button"
				on:click|preventDefault={() => {
					setWord(faker.commerce.productName());
				}}>Product</button
			>
			<button
				class="chip !bg-transparent"
				type="button"
				on:click|preventDefault={() => {
					setWord(faker.company.catchPhrase());
				}}>Catch Phrase</button
			>
			<button
				class="chip !bg-transparent"
				type="button"
				on:click|preventDefault={() => {
					setWord(faker.hacker.ingverb());
				}}>-ing Verb</button
			>
			<button
				class="chip !bg-transparent"
				type="button"
				on:click|preventDefault={() => {
					setWord(faker.word.interjection());
				}}>Exclamation</button
			>
			<button
				class="chip !bg-transparent"
				type="button"
				on:click|preventDefault={() => {
					setWord(faker.word.sample());
				}}>Random</button
			>
		</div>
	</div>
</div>

<style lang="postcss">
	figure {
		@apply flex relative flex-col;
	}
	figure img,
	.img-bg {
		@apply w-48 h-48 md:w-64 md:h-64;
	}
	.img-bg {
		@apply absolute z-[-1] rounded-full blur-[50px] transition-all;
		animation: pulse 5s cubic-bezier(0, 0, 0, 0.5) infinite, glow 5s linear infinite;
	}
	@keyframes glow {
		0% {
			@apply bg-primary-400/50;
		}
		33% {
			@apply bg-secondary-400/50;
		}
		66% {
			@apply bg-tertiary-400/50;
		}
		100% {
			@apply bg-primary-400/50;
		}
	}
	@keyframes pulse {
		50% {
			transform: scale(1.5);
		}
	}
</style>
