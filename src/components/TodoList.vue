<template>
  <div class="todo-list">
    <todo-list-item
        v-for="todo in todos"
        :todo="todo"
        :key="todo.id">
    </todo-list-item>
  </div>
</template>

<script>
import TodoListItem from "@/components/TodoListItem";

export default {
  name: "TodoList",
  components: {TodoListItem},
  props: ['todos']
}
</script>

<style scoped>
.todo-list {
  display: grid;
  row-gap: 14px;
}
</style>
