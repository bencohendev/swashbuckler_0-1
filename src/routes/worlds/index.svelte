<script>
	import { user } from '*stores/user';
	import { supabase } from '*lib/supabaseClient';

	let value = '';
	let worlds = [];
	const handleCreateWorld = async () => {
		try {
			const { data, error } = await supabase
				.from('worlds')
				.insert({ name: value, owner_id: $user.id });
			console.log('success!', data);
		} catch (error) {
			console.error(error);
		}
	};

	const handleGetWorlds = async () => {
		try {
			let { data, error } = await supabase.from('worlds').select('*');
			console.log('success!', data);
			worlds = data;
		} catch (error) {
			console.error(error);
		}
	};
</script>

<div class="mt-8">
	<h1>worlds</h1>

	<div>
		<input class="border  border-black" type="text" bind:value />
	</div>
	<button class="border  border-black" on:click={handleCreateWorld}
		>create new world</button
	>

	<button class="border  border-black" on:click={handleGetWorlds}
		>get worlds</button
	>
</div>

<div>
	{#each worlds as world}
		<div>{world.name}</div>
	{/each}
</div>
