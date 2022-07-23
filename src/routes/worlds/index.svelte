<script>
	import { user } from '*stores/user';
	import { supabase } from '*lib/supabaseClient';

	let value = '';

	const handleCreateWorld = async () => {
		user.set(supabase.auth.user());
		try {
			const { data, error } = await supabase
				.from('worlds')
				.insert([{ name: value }]);
			// console.log('success!', data);
		} catch (error) {
			console.error(error);
		}
	};
</script>

<div class="m-20">
	<h1>worlds</h1>

	<div class="my-8">
		<input class="border  border-black" type="text" bind:value />
	</div>
	<button class="border  border-black" on:click={handleCreateWorld}
		>create new world</button
	>
</div>
