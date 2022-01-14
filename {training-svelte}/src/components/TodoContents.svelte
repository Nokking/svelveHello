<script>
    import { todos } from '../stores/todo'
    import SelectTab from './SelectTab.svelte'

    let current = 'all'

    const validDoneFlag = (id) => {
        todos.update((todos) => {
            const result = todos.map((todo) => {
                if(todo.id === id){
                    todo.isDone = true
                }
                return todo
            })
            return result
        })
    }    

    $:resultTodoArr = $todos.filter(value => {
        if(current === 'done') return value.isDone === true
        if(current === 'notDone') return value.isDone === false
        return value
    })

    const changeCurrentStatus = (event) => {
        current = event.detail
    }

</script>

<div class="main_contents">
    <SelectTab
        on:changeCurrentStatus={changeCurrentStatus}
        current={current}/>
        <ul class="main_contents_list">
            {#if resultTodoArr.length === 0}
                <p class="main_contents_zerocase">0 items.</p>
            {:else}
                {#each resultTodoArr as todo}
                    <li class="main_contents_list_item">
                        <p  style={ todo.isDone ? 'text-decoration: line-through;' : ''}
                            class="main_contents_list_item-ttl">
                            {todo.text}
                        </p>
                        <button
                            on:click={validDoneFlag(todo.id)}
                            style={ todo.isDone ? 'background-color: #C7C7C7' : '' }
                            disabled={todo.isDone}
                            class="main_contents_list_item_button">
                            完了
                        </button>
                    </li>
                {/each}
            {/if}
        </ul>
</div>
