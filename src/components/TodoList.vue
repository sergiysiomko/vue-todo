<template>
  <div class="todo-list">
    <div>
      <form v-on:submit.prevent="submitForm">
        <input type="text" v-model="newTodoText" />
        <input type="submit" value="add" />
      </form>
    </div>
    <select v-model="todosOption">
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="uncompleted">Uncompleted</option>
    </select>

    <div v-if="filterTodos.length">
      <TodoItem
        v-for="todo in filterTodos"
        v-bind:key="todo.id"
        v-bind:todo="todo"
        v-on:remove-todo="removeTodo"
      />
    </div>
    <div v-else>0 todos</div>
  </div>
</template>

<script>
import TodoItem from "./TodoItem";
const TODOS_OPTIONS = {
  ALL: "all",
  COMPLETED: "completed",
  UNCOMPLETED: "uncompleted",
};

export default {
  name: "TodoList",
  props: ["todos"],
  components: { TodoItem },
  data() {
    return {
      newTodoText: "",
      todosOption: TODOS_OPTIONS.ALL,
    };
  },
  computed: {
    filterTodos: function () {
      if (this.todosOption === TODOS_OPTIONS.ALL) {
        return this.todos;
      }
      if (this.todosOption === TODOS_OPTIONS.COMPLETED) {
        return this.todos.filter((todo) => todo.completed);
      }
      if (this.todosOption === TODOS_OPTIONS.UNCOMPLETED) {
        return this.todos.filter((todo) => !todo.completed);
      }
    },
  },
  methods: {
    removeTodo(id) {
      this.$emit("remove-todo", id);
    },
    submitForm() {
      if (this.newTodoText.length) {
        this.$emit("submit-form", this.newTodoText);
        this.newTodoText = "";
      }
    },
  },
};
</script>

<style scoped>
.todo-list {
  width: 50%;
  max-width: 400px;
  margin: 0 auto;
}
</style>