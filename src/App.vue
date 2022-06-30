<template>
  <main>
    <div class="container">
      <h1>欢迎使用 Todo 待办事项！</h1>
      <todo-add :addTodo="addTodo"></todo-add>
      <todo-footer :todos="todos" :checkAllTodos="checkAllTodos" :deleteAllTodo="deleteAllTodo"></todo-footer>
      <todo-list :todos="todos" :checkTodo="checkTodo" :deleteTodo="deleteTodo"></todo-list>
    </div>
  </main>
</template>

<script>
import TodoAdd from "@/components/TodoAdd";
import TodoFooter from "@/components/TodoFooter";
import TodoList from "@/components/TodoList";

export default {
  name: 'App',
  components: {
    TodoList,
    TodoFooter,
    TodoAdd,
  },
  data() {
    return {
      //由于todos是MyHeader组件和MyFooter组件都在使用，所以放在App中（状态提升）
      todos: JSON.parse(localStorage.getItem('todos')) || []
    }
  },
  methods: {
    //添加一个todo
    addTodo(todo) {
      this.todos.unshift(todo)
    },
    //勾选or取消勾选一个todo
    checkTodo(id) {
      this.todos.forEach((todo) => {
        if (todo.id === id) todo.mode = !todo.mode
      })
    },
    //删除一个todo
    deleteTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id)
    },
    //全选or取消全选
    checkAllTodos(mode) {
      this.todos.forEach((todo) => {
        todo.mode = mode
      })
    },
    //清除所有已经完成的todo
    deleteAllTodo() {
      this.todos = this.todos.filter((todo) => {
        return !todo.mode
      })
    }
  },
  watch: {
    todos: {
      deep: true,
      handler(value) {
        localStorage.setItem('todos', JSON.stringify(value))
      }
    }
  },
}
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-family: Helvetica, "PingFang SC", "Microsoft Yahei", sans-serif;
}

/* 整个页面 */
main {
  width: 100vw;
  min-height: 100vh;
  padding: 10vh 0;
  display: grid;
  align-items: start;
  justify-items: center;
  background-color: rgb(222, 234, 246);
}

.container {
  width: 80%;
  max-width: 800px;
  box-shadow: 0px 0px 24px rgba(0, 0, 0, 0.15);
  padding: 48px 28px;
  position: relative;
  background-color: rgb(222, 234, 246);
  box-shadow: rgb(190, 203, 216) 12px 12px 24px 0px, rgb(243, 249, 255) -12px -12px 24px 0px;
  -webkit-box-shadow: rgb(190, 203, 216) 12px 12px 24px 0px, rgb(243, 249, 255) -12px -12px 24px 0px;
  border-radius: 40px;
  -webkit-border-radius: 40px;
}

/* 标题 */
h1 {
  margin: 24px 0;
  font-size: 28px;
  color: #4592af;
}
</style>
