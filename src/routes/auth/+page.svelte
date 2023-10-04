<!-- // src/routes/auth/+page.svelte -->
<script>
	import { goto } from '$app/navigation';
	import { redirect } from '@sveltejs/kit';

	export let data;
	let { supabase } = data;
	$: ({ supabase } = data);
	

	let email = '';
	let password = '';

	const handleSignUp = async () => {
		await supabase.auth.signUp({
			email,
			password,
			options: {
				emailRedirectTo: `${location.origin}/`
			}
		});
	};

	const handleSignIn = async () => {
		await supabase.auth.signInWithPassword({
			email,
			password
		});
	};

	const handleSignOut = async () => {
		await supabase.auth.signOut();
	};
</script>

<!-- <form
	on:submit|preventDefault={handleSignUp}
	class="flex flex-col mx-32 bg-red-100 px-10 py-4 w-fit border-2 border-red-200 rounded-md my-4"
>
	<div class="flex gap-4 items-center">
		<label for="email">Email</label>
		<input name="email" id="email" type="email" bind:value={email} />
	</div>
	<div class="flex gap-4 items-center">
		<label for="password">Password</label>
		<input type="password" name="password" id="password" bind:value={password} />
	</div>
	<div>
		<button type="submit">Sign up</button>
	</div>
</form>

<div class="flex m-3 gap-4">
	<button on:click={handleSignIn}>Sign in</button>
	<button on:click={handleSignOut}>Sign out</button>
</div>

<style>
	input {
		display: block;
		margin: 10px;
		border: 1px solid black;
	}
	button {
		padding: 3px 6px;
		border: 1px solid black;
		border-radius: 5px;
	}
</style> -->
<!--
  This example requires some changes to your config:
  
  ```
  // tailwind.config.js
  module.exports = {
    // ...
    plugins: [
      // ...
      require('@tailwindcss/forms'),
    ],
  }
  ```
-->
<!--
  This example requires updating your template:

  ```
  <html class="h-full bg-white">
  <body class="h-full">
  ```
-->
<div class="flex min-h-full flex-col justify-center px-6 py-12 lg:px-8">
	<div class="sm:mx-auto sm:w-full sm:max-w-sm">
		<img
			class="mx-auto h-20 w-auto rounded-xl"
			src="https://i.pinimg.com/564x/30/11/b2/3011b2705563a38655c2b37ce0db6ed1.jpg"
			alt="Your Company"
		/>
		<h2 class="mt-5 text-center text-3xl font-bold leading-9 tracking-tight text-gray-900">
			Simple Auth
		</h2>
	</div>

	<div class="mt-10 sm:mx-auto sm:w-full sm:max-w-sm">
		<form class="space-y-6">
			<div>
				<label for="email" class="block text-sm font-medium leading-6 text-gray-900"
					>Email address</label
				>
				<div class="mt-2">
					<input
						bind:value={email}
						id="email"
						name="email"
						type="email"
						autocomplete="email"
						class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6 outline-none px-3"
					/>
				</div>
			</div>

			<div>
				<div class="flex items-center justify-between">
					<label for="password" class="block text-sm font-medium leading-6 text-gray-900"
						>Password</label
					>
				</div>
				<div class="mt-2">
					<input
						bind:value={password}
						id="password"
						name="password"
						type="password"
						autocomplete="current-password"
						class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6 outline-none px-3"
					/>
				</div>
			</div>

			<div class="flex gap-4">
				<button
					on:click={handleSignUp}
					class="flex w-full justify-center rounded-md bg-indigo-600 px-3 py-1.5 text-sm font-semibold leading-6 text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
					>Sign Up</button
				>
				<button
					on:click={handleSignIn}
					class="flex w-full justify-center rounded-md bg-indigo-600 px-3 py-1.5 text-sm font-semibold leading-6 text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
					>Sign in</button
				>
				<button
					on:click={handleSignOut}
					class="flex w-full justify-center rounded-md bg-indigo-600 px-3 py-1.5 text-sm font-semibold leading-6 text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
					>Sign Out</button
				>
			</div>
		</form>
	</div>
</div>
