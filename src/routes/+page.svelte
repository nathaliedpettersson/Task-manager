<script>
    let newTask = "";

    let DUMMY_TASKS = [
        { text: "First task", status: true },
        { text: "Second task", status: false },
        { text: "Third task", status: false },
    ];

    function addNewTask() {
        DUMMY_TASKS = [...DUMMY_TASKS, { text: newTask, status: false }];
        newTask = "";
    }

    function removeTask(index) {
        DUMMY_TASKS.splice(index, 1);
        DUMMY_TASKS = DUMMY_TASKS;
    }
</script>

<input bind:value={newTask} type="text" placeholder="My next task..." />
<button on:click={addNewTask}>Add</button>

<br />
{#each DUMMY_TASKS as item, index}
    <input bind:checked={item.status} type="checkbox" />
    <span class:checked={item.status}>{item.text}</span>
    <button on:click={() => removeTask(index)}>❌</button>
    <br />
{/each}

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
