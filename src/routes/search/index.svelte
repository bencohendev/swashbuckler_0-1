<script>
	import { supabase } from '*lib/supabaseClient';
	import Button from '*c/Button.svelte';

	let value = '';

	const handleSearch = async () => {
		try {
			const { data, error } = await supabase
				.from('worlds')
				.select()
				.textSearch('name', `${value}`);
			console.log(data, error);
		} catch (error) {
			console.error(error);
		}
	};
</script>

<div class="mt-8">
	<h1 class="text-xl font-bold">search</h1>
	<div>input search term</div>
	<div class="my-8">
		<input class="border  border-black" type="text" bind:value />
	</div>
	<Button on:click={handleSearch}>search</Button>
</div>
