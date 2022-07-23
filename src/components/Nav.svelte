<script>
	let links = [
		{
			label: 'Home',
			url: './'
		},
		{
			label: 'worlds',
			url: './worlds'
		}
	];
</script>

<div class="grid justify-between grid-flow-row">
	{#each links as link}
		{@const { url, label } = link}
		<div><a class="text-blue-500" href={url}>{label}</a></div>
	{/each}
</div>
