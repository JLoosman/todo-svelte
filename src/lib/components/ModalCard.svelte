<script>
    import { slide } from 'svelte/transition'
    import {todo} from '../stores/todoStore'

    export let singleTask = {}

    // redeclare store when input is made
    const updateStore = () => {
        todo.update((item) => [...item])
    }
</script>

<div transition:slide class="modal">
    <form>
        <div class="column">
            <textarea bind:value={singleTask.description} on:input={updateStore} name="description" id="description" maxlength=250 placeholder="Description..."></textarea>

            <div class="inline">
                <label for="important">Wichtig:</label>
                <input bind:checked={singleTask.important} on:change={updateStore} id="important" type="checkbox">
            </div>
            <div class="inline">
                <label for="urgent">Dringend:</label>
                <input bind:checked={singleTask.urgent} on:change={updateStore} id="urgent" type="checkbox">
            </div>
            <div class="inline">
                <label for="progress">Progress in %:</label>
                <input  type="number" bind:value={singleTask.progress} on:input={updateStore} id="progress" min=0 max=100>
            </div>
        </div>
        <div class="column">
            <div class="inline">
                <label for="author">Author:</label>
                <input bind:value={singleTask.author} on:input={updateStore} id="author" type="text" placeholder="Author..." maxlength="50">
            </div>
            <div class="inline">
                <label for="category">Category:</label>
                <select bind:value={singleTask.category} on:change={updateStore} name="category" id="category">
                    <option selected disabled value="Category">Category</option>
                    <option value="Sport">Sport</option>
                    <option value="Food">Food</option>
                    <option value="Health">Health</option>
                    <option value="Lernen">Lernen</option>
                    <option value="Reisen">Reisen</option>
                </select>
            </div>
            <div class="inline">
                <label for="startDate">Start:</label>
                <input bind:value={singleTask.startDate} on:input={updateStore} id="startDate" type="date">
            </div>
            <div class="inline">
                <label for="endDate">End:</label>
                <input bind:value={singleTask.endDate} on:input={updateStore} id="endDate" type="date">
            </div>
        </div>
    </form>
</div>

<style>
    .modal {
        margin-right: 61.6px;
        padding: 5px 20px 30px;
        border-radius: 10px;
        color: var(--white);
        background: var(--primary-color);
        box-shadow: 0 4px 5px #646FF033;
    }

    form {
        display: flex;
    }

    .column {
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        padding: 20px 20px;
        height: 250px;
        width: 50%;
    }

    @media screen and (max-width: 750px) {
        form {
            display: flex;
            flex-direction: column;
        }

        .column {
            width: 100%;
        }
    }

    .inline {
        display: flex;
        justify-content: space-between;
        align-items: center;
    }

    input {
        padding: 5px 10px;
        border: none;
        border-radius: 10px;
        width: 60%;
    }

    input[type="checkbox"] {
        width: initial;
        margin-right: 5px;
        transform: scale(1.5);
    }

    input[type="number"] {
        width: 30%;
    }

    textarea {
        padding: 5px 10px;
        border: none;
        border-radius: 10px;
    }

    select {
        padding: 5px 10px;
        border: none;
        border-radius: 10px;
        width: 60%;
    }

</style>