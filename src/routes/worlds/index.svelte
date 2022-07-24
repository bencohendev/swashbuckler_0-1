<script>
	import { user } from '*stores/user';
	import { supabase } from '*lib/supabaseClient';
	import Button from '*c/Button.svelte';

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
	<h1 class="text-xl font-bold">worlds</h1>

	<div class="my-8">
		<input class="border  border-black" type="text" bind:value />
	</div>
	<Button on:click={handleCreateWorld}>create new world</Button>

	<Button sveltekit:prefetch on:click={handleGetWorlds}>get worlds</Button>
</div>
<div>
	{#each worlds as world}
		<Button><a href="./worlds/{world.id}">{world.name}</a></Button>
	{/each}
</div>
