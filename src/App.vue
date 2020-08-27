<template>
  <div id="app">
    <TodoList v-bind:todos="todos" @remove-todo="removeTodo" @submit-form="addTodo" />
  </div>
</template>

<script>
import TodoList from "./components/TodoList";
export default {
  name: "App",
  components: { TodoList },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter((t) => t.id !== id);
    },
    addTodo(text) {
      const id = Date.now();

      this.todos.push({ id, text, completed: false });
    },
  },
  data() {
    return {
      todos: [
        { id: 1, text: "asd a;skdfj", completed: false },
        { id: 2, text: "asd a;skdfj", completed: false },
        { id: 3, text: "asd a;skdfj", completed: false },
      ],
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
