<script>
	import { user } from '*stores/user';
	import { supabase } from '*lib/supabaseClient';
	import Test from '*lib/Test.svelte';
	import Auth from '*lib/Auth.svelte';
	import Profile from '*lib/Profile.svelte';

	user.set(supabase.auth.user());

	supabase.auth.onAuthStateChange((_, session) => {
		user.set(session.user);
	});
	$: console.log($user);
</script>

<div class="container" style="padding: 50px 0 100px 0;">
	ben <Test />
	{#if $user}
		<Profile />
	{:else}
		<Auth />
	{/if}
</div>
