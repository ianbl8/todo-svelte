<script>
  import { v4 as uuidv4 } from 'uuid';
  import Title from "./Title.svelte";
  import Todolist from './Todolist.svelte';
  import AddTodoForm from './AddTodoForm.svelte';
 
  let todoText = "";
  let todoItems = [];
  let doneItems = [];

  function addTodo(todoText) {
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
  <Title title="Simple Todo List" subtitle="Fun Things to do"/>1
  <div class="section box">
    <AddTodoForm addTodo="{addTodo}" />
  </div>
  <Todolist caption="Tasks to do" items="{todoItems}" deleteHandler="{deleteTodo}"/>
  <Todolist caption="Tasks done" items="{doneItems}"/>
</div>