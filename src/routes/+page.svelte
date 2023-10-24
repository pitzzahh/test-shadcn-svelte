<script>
	import Hero from '$lib/components/Hero.svelte';
	import { onMount } from 'svelte';
	import * as Table from '$lib/components/ui/table';
	import { Button } from '$lib/components/ui/button';
	/**
	 * @type {any[]}
	 */
	let users = [];
	onMount(() => {
		fetch('https://dummyjson.com/users?limit=100')
			.then((res) => res.json())
			.then((json) => {
				users = json.users;
				console.log('Fetched');
				console.log(users);
			});
	});
</script>

<Hero />
<Table.Root>
	<Table.Caption>A list of your recent invoices.</Table.Caption>
	<Table.Header>
		<Table.Row>
			<Table.Head class="w-[100px]">First Name</Table.Head>
			<Table.Head>Last Name</Table.Head>
			<Table.Head>Maiden Name</Table.Head>
			<Table.Head class="text-right">Age</Table.Head>
		</Table.Row>
	</Table.Header>
	<Table.Body>
		{#each users as user, i (i)}
			<Table.Row on:click={() => console.log('Clicked row')}>
				<Table.Cell class="font-medium">{user.firstName}</Table.Cell>
				<Table.Cell>{user.lastName}</Table.Cell>
				<Table.Cell>{user.maidenName}</Table.Cell>
				<Table.Cell class="text-right">{user.age}</Table.Cell>
				<Button class="self-end">Delete</Button>
			</Table.Row>
		{/each}
	</Table.Body>
</Table.Root>
