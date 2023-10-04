<script>
	export let data;
	let { supabase } = data;
	$: ({ supabase } = data);

	const handleSignOut = async () => {
		await supabase.auth.signOut();
	};
</script>

<div class=" md:px-20">
	<h1 class="text-3xl font-bold my-3">Auth using Sveltekit + Supabase</h1>
	<div class="flex gap-3">
		<button class="hover:bg-zinc-200/30">{data.session?.user.email || 'No User'}</button>
		{#if data.session?.user.email}
			<button class="hover:bg-zinc-100" on:click={handleSignOut}>Sign Out</button>
		{/if}
	</div>
	<div><a href="/auth">Login</a> to continue...</div>
</div>

<style>
	button {
		display: block;
		margin: 5px 0;
		border: 1px solid black;
		padding: 3px 6px;
	}
	a {
		text-decoration: underline;
		font-weight: 600;
	}
</style>
