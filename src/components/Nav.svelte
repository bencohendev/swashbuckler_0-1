<script>
	let links = [
		{
			label: 'Home',
			url: '/'
		},
		{
			label: 'worlds',
			url: '/worlds'
		},
		{
			label: 'realtime test',
			url: '/realtime'
		}
	];
</script>

<div class="flex border">
	{#each links as link}
		{@const { url, label } = link}
		<div class="mr-8"><a class="text-blue-500" href={url}>{label}</a></div>
	{/each}
</div>
