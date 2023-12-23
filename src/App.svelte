<script>
	import Modal from './Modal.svelte';
	import AddPersonForm from './AddPersonForm.svelte';

	let showModal = false;

	const toggleModal = () => {
		showModal = !showModal;
	}

	let people = [
		{ name: 'Wesley', beltColor: 'black', age: 27, id: 1 },
		{ name: 'Sarah', beltColor: 'brown', age: 28, id: 2},
		{ name: 'Mike', beltColor: 'blue', age: 29, id: 3 }
	];

	const handleClick = (id) => {
		people = people.filter(person => person.id != id)
	};

	const addPerson = (e) => {
		const person = e.detail;
		people = [...people, person];
		// to close the Modal after adding a person
		showModal = false;
	};
</script>

<Modal {showModal} on:click={toggleModal}>
	<AddPersonForm on:addPerson={addPerson} />
</Modal>
<main>
	<button on:click={toggleModal}>Open Modal</button>
	{#each people as person (person.id)}
		<div>
			<h4>{person.name}</h4>
			{#if person.beltColor === 'black'}
				<p><strong>MASTER NINJA</strong></p>
			{/if}
			<p>{person.age} years old, {person.beltColor} belt</p>
			<button on:click={() => handleClick(person.id)}>delete</button>
		</div>
	{:else}
		<p>There are no people to show...</p>
	{/each}
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>