<script>
// @ts-nocheck

import Select from "./Select.svelte";
import { afterUpdate } from 'svelte';
   
    let newTask = "";
    let estimatedTime;
    /**
     * @type {any}
     */
    let selected;

    let DUMMY_TASKS = [
        { text: "First task", time: 1, weekday: "Monday", status: true },
        { text: "Second task", time: 3, weekday: "Tuesday", status: false },
        { text: "Third task", time: 6, weekday: "Wednesday", status: false },
    ];

    function addNewTask() {
        DUMMY_TASKS = [...DUMMY_TASKS, { text: newTask, time: estimatedTime, weekday: selected, status: false }];
        newTask = "";
    }

    // @ts-ignore
    function removeTask(index) {
        DUMMY_TASKS.splice(index, 1);
        DUMMY_TASKS = DUMMY_TASKS;
    }

    $: sumOfAllTasks = DUMMY_TASKS.reduce((acc , t) => acc + t.time, 0);

</script>

<input bind:value={newTask} type="text" placeholder="My next task..." />
<input bind:value={estimatedTime} type="num" placeholder="Estimated time in hours" />
<Select id="weekday" name="weekday" bind:value={selected}>
	<option value="monday">Mon</option>
	<option value="tuesday">Tues</option>
    <option value="wednesday">Wed</option>
	<option value="thursday">Thurs</option>
    <option value="friday">Fri</option>
</Select>
<button on:click={addNewTask}>Add</button>

<br />
{#each DUMMY_TASKS as item, index}
    <input bind:checked={item.status} type="checkbox" />
    <span class:checked={item.status}>{item.text} {item.time} {item.weekday}</span>
    <button on:click={() => removeTask(index)}>❌</button>
    <br />
{/each}

<p>
    Your current tasks will take {sumOfAllTasks} hours.
  </p>

<style>
    .checked {
        text-decoration: line-through;
    }
</style>

<!-- 
Plan for this app is: 

- Figure out how to add weekday when adding task, and filter this in the right column 
- Handle deleting tasks differently depending on which day you're on
- How to store my tasks? Local storage or some database? 
- Look into adding a field for time and also set some default time/day for example 12 hours (this should also calculate each tasks time that day) 
- Styling ofc  -->
