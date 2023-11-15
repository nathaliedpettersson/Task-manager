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
