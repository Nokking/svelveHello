<script>
    import { todos } from '../stores/todo'
  
    let text = ''
    let errorMessage = ''
  
    const registerTodo = () => {
      if(text === '') {
        errorMessage = 'TODOが入力されていません。TODOを入力してください。'
        return
      }
      const id = $todos.length + 1
  
      errorMessage = ''
      todos.update((todo) => {
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
  
  <style>
  .main_form {
    width: 800px;
    margin: 100px auto 0;
  }
  .main_form_body {
    display: flex;
    justify-content: space-between;
  }
  .main_form_error {
    padding: 0 0 5px 5px;
    font-size: 14px;
    font-weight: 100;
    color: #ff5c5c;
  }
  .main_form_txt {
    width: 700px;
    padding: 12px 0;
    padding-left: 20px;
    font-size: 20px;
    border-radius: 7px;
    color: #000;
    border: 1px solid #707070;
    background-color: #fff;
  }
  .main_form_submit {
    display: block;
    width: 70px;
    border-radius: 7px;
    padding: 12px 18px;
    color: #000;
    border: 1px solid #707070;
    background-color: #fff;
  }
  </style>