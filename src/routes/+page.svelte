<script>
    // @ts-nocheck
    
    import Select from "./Select.svelte";
    
    let newTask = "";
    let estimatedTime;
    /**
     * @type {any}
     */
    let selected;
    
    let WEEKDAY_TASKS = {
        monday: [],
        tuesday: [],
        wednesday: [],
        thursday: [],
        friday: [],
    };
    
    function addNewTask() {
        WEEKDAY_TASKS = { ...WEEKDAY_TASKS, [selected]: [...WEEKDAY_TASKS[selected], { text: newTask, time: Number(estimatedTime), status: false }] };
        newTask = "";
    }
    
    // @ts-ignore
    function removeTask(weekday, index) {
        WEEKDAY_TASKS = { ...WEEKDAY_TASKS, [weekday]: WEEKDAY_TASKS[weekday].filter((_, i) => i !== index) };
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

  <div id="container">
    <div>Monday</div>
    <div>Tuesday</div>
    <div>Wednesday</div>
    <div>Thursday</div>
    <div>Friday</div>
  </div>

<style>
    .checked {
        text-decoration: line-through;
    }

    #container {
        display: flex;
        flex-direction: row;
        flex-wrap: nowrap;
    }

    #container div {
        border: 2px solid black;
        width: 20vw;
    }
</style>

<!-- 
Plan for this app is: 

- Figure out how to add weekday when adding task, and filter this in the right column 
- Handle deleting tasks differently depending on which day you're on
- How to store my tasks? Local storage or some database? 
- Look into adding a field for time and also set some default time/day for example 12 hours (this should also calculate each tasks time that day) 
- Styling ofc  -->
