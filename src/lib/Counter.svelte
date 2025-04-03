<script>
  let todos = [];
  let newTodoText = '';

  function addTodo() {
    const text = newTodoText.trim();
    if (!text) return;

    todos = [...todos, { id: Date.now(), text: text, completed: false }];
    newTodoText = '';
  }

  function removeTodo(idToRemove) {
    todos = todos.filter(todo => todo.id !== idToRemove);
  }
</script>

<main>
  <h1>svelte to-do app</h1>

  <form on:submit|preventDefault={addTodo} class="add-form">
    <input
      type="text"
      bind:value={newTodoText}
      placeholder="Add a new task"
      aria-label="New todo input"
    />
    <button type="submit">Add</button>
  </form>

  <ul class="todo-list">
    {#each todos as todo (todo.id)}
      <li class:completed={todo.completed}>
        <input
          type="checkbox"
          bind:checked={todo.completed}
          aria-label={`Mark ${todo.text} as ${todo.completed ? 'incomplete' : 'complete'}`}
        />
        <span class="todo-text">{todo.text}</span>
        <button class="remove-button" on:click={() => removeTodo(todo.id)} aria-label={`Remove ${todo.text}`}>
          &times;
        </button>
      </li>
    {/each}
  </ul>
</main>

<style>
  main {
    max-width: 400px;
    margin: 30px auto;
    padding: 20px;
    font-family: sans-serif;
    border: 1px solid #ddd;
    border-radius: 5px;
    background: #f9f9f9;
  }
  h1 {
    text-align: center;
    color: #333;
    margin-bottom: 20px;
  }
  .add-form {
    display: flex;
    margin-bottom: 15px;
  }
  .add-form input {
    flex-grow: 1;
    padding: 8px;
    border: 1px solid #ccc;
    border-radius: 3px 0 0 3px;
  }
  .add-form button {
    padding: 8px 12px;
    border: none;
    background-color: #28a745;
    color: white;
    cursor: pointer;
    border-radius: 0 3px 3px 0;
  }
  .todo-list {
    list-style: none;
    padding: 0;
    margin: 0;
  }
  .todo-list li {
    display: flex;
    align-items: center;
    padding: 8px 5px;
    border-bottom: 1px solid #eee;
  }
  .todo-list li:last-child {
    border-bottom: none;
  }
  .todo-list input[type="checkbox"] {
    margin-right: 10px;
    cursor: pointer;
  }
  .todo-list span.todo-text {
    flex-grow: 1;
    word-break: break-all;
    color: black;
  }
  .todo-list li.completed span.todo-text {
    text-decoration: line-through;
    color: #888;
  }
  .remove-button {
    background: none;
    border: none;
    color: #dc3545;
    font-size: 1.2rem;
    cursor: pointer;
    padding: 0 5px;
    margin-left: 5px;
    opacity: 0.6;
  }
  .remove-button:hover {
    opacity: 1;
  }
</style>