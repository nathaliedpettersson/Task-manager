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
    
    $: sumOfAllTasks = Object.values(WEEKDAY_TASKS).reduce((acc, weekdayTasks) => {
        return acc + weekdayTasks.reduce((total, task) => total + task.time, 0);
    }, 0);
    
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
    {#each Object.entries(WEEKDAY_TASKS) as [weekday, tasks]}
        {#if tasks.length > 0}
            <h3>{weekday}</h3>
            {#each tasks as task, index}
                <input bind:checked={task.status} type="checkbox" />
                <span class:checked={task.status}>{task.text} {task.time} hours</span>
                <button on:click={() => removeTask(weekday, index)}>❌</button>
                <br />
            {/each}
        {/if}
    {/each}
    
    <p>
        Your current tasks will take {sumOfAllTasks} hours.
    </p>
    
<style>
    .checked {
        text-decoration: line-through;
    }
</style>


