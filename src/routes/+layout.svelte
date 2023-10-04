<script lang="ts">
	import '../app.postcss';
	import { invalidate } from '$app/navigation';
	import { onMount } from 'svelte';
	import type { LayoutData } from './$types';

	export let data: LayoutData;

	$: ({ supabase, session } = data);

	onMount(() => {
		const {
			data: { subscription }
		} = supabase.auth.onAuthStateChange((event, _session) => {
			if (_session?.expires_at !== session?.expires_at) {
				invalidate('supabase:auth');
			}
		});

		return () => subscription.unsubscribe();
	});
</script>

<nav>
	<ul class="flex gap-4 py-4">
		<li>
			<a href="/">Home</a>
		</li>
		<li>
			<a href="/auth">Login</a>
		</li>
	</ul>
</nav>
<slot />

<style>
	nav {
		display: flex;
		background: rgb(206, 254, 252);
		justify-content: center;
	}
	li a {
		text-decoration: none;
		color: black;
		font-size: 1.06rem;
	}
	a:hover{
		color : rgb(0, 81, 255);
	}
</style>
