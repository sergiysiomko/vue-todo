<template>
  <div class="todo-item">
    <input type="checkbox" v-on:change="todo.completed = !todo.completed" />
    <span class="text" v-bind:class="{done:todo.completed}">{{todo.text}}</span>
    <button v-on:click="$emit('remove-todo', todo.id)">X</button>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: {
    todo: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style scoped>
.todo-item {
  display: flex;
  justify-content: space-between;
}
.text.done {
  text-decoration: line-through;
}
</style>