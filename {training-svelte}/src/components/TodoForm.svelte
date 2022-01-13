<script>
    import { todos } from '../stores/todo'
    

    let text = ''
    let errorMessage = ''

    const registerTodo = () => {
        if(text === ''){
            errorMessage = 'Text not found.'
            return
        }
        errorMessage = ''
        const id = $todos.length + 1
        todos.update((todo)=> {
            return [...todo, {id, text, 'isDone': false}]
        })

        text = ''
    }

</script>

<div class="main_form">
    {#if errorMessage}
        <p class="main_form_error">{errorMessage}</p>    
    {/if}
    <form class="main_form_body">
        <input 
            bind:value={text} 
            class="main_form_txt" 
            type="text" 
            placeholder="TODO">
        <button 
            on:click={registerTodo} 
            class="main_form_submit" 
            type="button">
        追加
        </button>
    </form>
</div>