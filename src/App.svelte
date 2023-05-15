<script>
  let todoText = "";
  let todoItems = [];
  let doneItems = [];

  import { v4 as uuidv4 } from 'uuid';
  import Title from "./Title.svelte";
  import Todolist from './Todolist.svelte';
 
  function addTodo() {
    console.log(todoText)
    const todo = {
      text: todoText,
      date: new Date().toLocaleString("en-IE"),
      id: uuidv4(),
    };
    todoItems.push(todo);
    todoItems = [...todoItems];
    todoText = "";
  };

  function deleteTodo(id) {
    const found = todoItems.findIndex((todo) => todo.id == id);
    const done = todoItems[found];
    todoItems.splice(found, 1);
    todoItems = [...todoItems];
    doneItems.push(done);
    doneItems = [...doneItems];
  };
</script>

<div class="container">
  <Title title="Simple Todo List" subTitle="Fun Things to do"/>
  <div class="section box">
    <div class="field is-horizontal">
      <div class="field-label is-normal">
        <label for="todo" class="label">What should I do?</label>
      </div>
      <div class="field-body">
        <div class="field">
          <p class="control">
            <input bind:value={todoText} id="todo" class="input" type="text" placeholder="Type something...">
          </p>
        </div>
        <button on:click={addTodo} class="button">Add Todo</button>
      </div>
    </div>
  </div>
  <Todolist caption="Tasks to do" items="{todoItems}" deleteHandler="{deleteTodo}"/>
  <Todolist caption="Tasks done" items="{doneItems}"/>
</div>

