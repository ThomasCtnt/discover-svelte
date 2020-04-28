<script>
	import Modal from './Modal.svelte';
	import AddPersonForm from './AddPersonForm.svelte';
	
	let firstName = "John";
	let lastName = "Doe";
	let beltColour = "black";

	let showModal = false;

	/* 	
	* Reactive value declaration 
	* Doc: https://svelte.dev/tutorial/reactive-declarations
	* Example: https://svelte.dev/examples#reactive-declarations
	*/
	$: fullName = `${firstName} ${lastName}`;

	/* 
	* Will log the value of beltColour and the fullName 
	* in the console each time the value is updated
	*/
	$: {
		console.log(beltColour);
		console.log(fullName);
	}

	const handleCLick = () => {
		beltColour = 'orange';
	};

	const handleInput = (e) => {
		beltColour = e.target.value;
	};

	let people = [
		{ name: 'Jack', beltColour: 'black', age: 25, id: 1 },
		{ name: 'Josh', beltColour: 'orange', age: 45, id: 2 },
		{ name: 'Jace', beltColour: 'brown', age: 35, id: 3 }
	];

	const handleDelete = (id) => {
		// Delete the person from people
		people = people.filter((person) => person.id != id);
	};

	const toggleModal = () => {
		showModal = !showModal;
	};

	const addPerson = (e) => {
		const person = e.detail;
		people = [person, ...people];
		showModal = false;
	};
</script>

<Modal isPromo={true} {showModal} on:click={toggleModal}>
	<AddPersonForm on:addPerson={addPerson} />
</Modal>

<main>
	<button on:click|once={toggleModal}>Open modal</button>
	<p>{fullName} - {beltColour} belt</p>

	<input type="text" bind:value={firstName}>
	<input type="text" bind:value={lastName}>
	<input type="text" bind:value={beltColour}>

	{#each people as person (person.id)}
		<div>
			<h4>{person.name}</h4>
			{#if person.beltColour === 'black'}
				<strong>Karate Master</strong>
			{/if}
			<p>{person.age} years old, {person.beltColour} belt.</p>
			<button on:click={() => handleDelete(person.id)}>Delete</button>
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

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>