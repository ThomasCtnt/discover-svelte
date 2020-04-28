<script>
    import { createEventDispatcher } from 'svelte';

    let dispatch = createEventDispatcher();

    let name;
    let beltColour;
    let age;
    
    let skills = [];

    const handleSubmit = () => {
        const person = {
            name,
            beltColour,
            age,
            skills,
            id: Math.random()
        };

        // Dispatch a custom event with data
        dispatch('addPerson', person);
    }
</script>

<form on:submit|preventDefault={handleSubmit}>
    <input type="text" placeholder="Name" bind:value={name}>
    <input type="number" placeholder="Age" bind:value={age}>
    <label>Skills:</label>
    <input type="checkbox" bind:group={skills} value="fighting">Fighting<br>
    <input type="checkbox" bind:group={skills} value="sneaking">Sneaking<br>
    <input type="checkbox" bind:group={skills} value="running">Running<br>
    <label>Belt Colour:</label>
    <select bind:value={beltColour}>
        <option value="black">Black</option>
        <option value="brown">Brown</option>
        <option value="orange">Orange</option>
        <option value="white">White</option>
    </select>
    <button>Add person</button>
</form>

<style>

</style>