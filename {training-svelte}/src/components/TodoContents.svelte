<script>
    import { todos } from '../stores/todo'
    import  SelectTab from './SelectTab.svelte'
  
    let current = 'all'
  
    const validDoneFlag = (id) => {
      todos.update((todos) => {
        const result = todos.map((todo) => {
          if(todo.id === id) {
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
        <p class="main_contents_zerocase">0件やで？</p>
      {:else}
        {#each resultTodoArr as todo}
          <li class="main_contents_list_item">
          <p
            style={ todo.isDone ? 'text-decoration: line-through;' : ''  }
            class="main_contents_list_item-ttl">
              {todo.text}
            </p>
            <button
              on:click={validDoneFlag(todo.id)}
              style={ todo.isDone ? 'background-color: #C7C7C7;' : ''  }
              disabled={todo.isDone}
              class="main_contents_list_item-button">
              完了
            </button>
          </li>
        {/each}
      {/if}
    </ul>
  </div>
  
  <style>
  .main_contents {
    width: 800px;
    margin: 66px auto 0px;
  }
  .main_contents_zerocase {
    text-align: center;
    font-size: 18px;
    font-weight: 100;
    color: #ff5c5c;
  }
  .main_contents_list {
    margin-top: 40px;
  }
  .main_contents_list_item {
    position: relative;
    border-bottom: 1px solid #000;
    margin-top: 40px;
    padding: 0 110px 40px 0;
    display: flex;
    align-items: center;
  }
  
  .main_contents_list_item-ttl {
    font-size: 19px;
    padding-left: 20px;
    color: #000;
  }
  .main_contents_list_item-button {
    position: absolute;
    display: block;
    right: 20px;
    width: 73px;
    flex-shrink: 0;
    margin-left: 35px;
    font-size: 14px;
    text-align: center;
    padding: 11px 0;
    border-radius: 7px;
    color: #000;
    border: 1px solid #707070;
    background-color: #fff;
  }
  </style>