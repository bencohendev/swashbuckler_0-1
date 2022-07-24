<script>
	import { supabase } from '*lib/supabaseClient.js';
	import Editor from '*c/tiptap/Editor.svelte';
	let value = '';

	const subscribe = () => {
		const mySubscription = supabase
			.from('realtime')
			.on('*', (payload) => {
				console.log('Change received!', payload);
				if (value !== payload.new.value) value = payload.new.value;
			})
			.subscribe();
	};
	//subscribe();

	const changeVal = async () => {
		try {
			const { data, error } = await supabase
				.from('realtime')
				.update({ value, jVal: [{ label: 'input', value: value }] })
				.eq('id', 1);
			console.log('success!', data, error);
		} catch (error) {
			console.error(error);
		}
	};

	$: {
		if (value) changeVal();
	}

	const getInitialValue = async () => {
		let { data, error } = await supabase
			.from('realtime')
			.select('value')
			.eq('id', 1);

		value = data[0].value;
	};
	getInitialValue();
</script>

<h1 class="text-5xl font-bold">
	WARNING CHANGING DATA TOO FAST WILL CRASH THE APP
</h1>
<input class="border border-gray my-8" type="text" bind:value />

<div class="my-8">
	<div>see output below</div>
	<div class="my-2 text-red-500">{value}</div>
</div>

<div>
	<h1 class="text-xl font-bold">Tiptap Editor</h1>
	<div class="border border-black">
		<Editor />
	</div>
</div>
