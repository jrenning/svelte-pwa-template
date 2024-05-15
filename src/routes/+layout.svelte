<script lang="ts">
	import '../app.css';
	import { SignIn, SignOut } from '@auth/sveltekit/components';
	import { page } from '$app/stores';
	import { signIn } from '@auth/sveltekit/client';

	var today = new Date();
	var dd = String(today.getDate()).padStart(2, '0');
	var mm = String(today.getMonth() + 1).padStart(2, '0'); //January is 0!
	var yyyy = today.getFullYear();

	let todayString = mm + '/' + dd + '/' + yyyy;
</script>

<header
	class="flex flex-row items-center mt-6 justify-around mb-10 relative text-center w-full bg-surface-50 dark:bg-surface-900"
>
	{#if $page.data.session}
		<div class="flex flex-row justify-center space-x-5">
			<div
				class="rounded-full w-10 h-10 font-bold bg-gray-300 flex justify-center items-center text-black text-2xl"
			>
				J
			</div>
			<div class="flex justify-center font-semibold items-center">Jack Renning</div>
		</div>
		<div />
	{:else}
		<button class="rounded-md bg-primary-500 shadow-md px-2 py-1" on:click={() => signIn('google')}
			>Sign In With Google</button
		>
	{/if}
	<div class="flex flex-col">
		<div class="text-right font-semibold text-gray-400 italic">Today</div>
		<div class="font-semibold text-xl">
			{todayString}
		</div>
	</div>
</header>

{#if $page.data.session}
	<slot />
{/if}
