<template>
  <div class="todoList-item">
    <div class="todo-item">
      <label :style='decoration'>
        <input
            type="checkbox" :checked="todo.mode" @click="handleCheck(todo.id)"/>
        {{ todo.title }}
        <span class="check-button"></span>
        <button class="delete-button" @click="handleDelete(todo.id)">X</button>
      </label>
    </div>
  </div>
</template>

<script>
import pubsub from "pubsub-js"
export default {
  name: "TodoListItem",
  computed: {
    decoration() {
      if (this.todo.mode) {
        return 'text-decoration:line-through'
      }
      return 'text-decoration:none'
    }
  },
  props: ['todo'],
  methods: {
    handleCheck(id) {
      //通知App组件将对应的mode取反
      // this.checkTodo(id)
      pubsub.publish('checkTodo',id)
    },
    handleDelete(id) {
      //通知App组件将对应的todo对象删除
      // this.deleteTodo(id)
      pubsub.publish('deleteTodo',id)
    }
  }
}
</script>

<style scoped>
.todo-item {
  padding: 16px;
  border-radius: 40px;
  color: #626262;
  background-color: #deeaf6;
  box-shadow: rgba(163, 177, 198, 0.5) 12px 12px 24px 0px, rgb(255, 255, 255) -12px -12px 24px 0px;
  -webkit-box-shadow: rgba(163, 177, 198, 0.5) 12px 12px 24px 0px, rgb(255, 255, 255) -12px -12px 24px 0px;
  border-radius: 40px;
  -webkit-border-radius: 40px;
}

.todo-item label {
  position: relative;
  display: flex;
  color: #4592af;
  align-items: center;
  cursor: pointer;
}

.todo-item label span.check-button {
  position: absolute;
  top: 0;
}

.delete-button {
  background: none;
  border: none;
  position: absolute;
  right: 10px;
  color: #ff5858;
  font-weight: bold;
}

.delete-button:active {
  transform: translateY(-3px);
}

.todo-item label span.check-button::before,
.todo-item label span.check-button::after {
  content: "";
  display: block;
  position: absolute;
  width: 18px;
  height: 18px;
  border-radius: 50%;
}

.todo-item label span.check-button::before {
  border: 1px solid #4592af;
}

.todo-item label span.check-button::after {
  transition: 0.4s;
  background: #4592af;
  transform: translate(1px, 1px) scale(0.8);
  opacity: 0;
}

.todo-item input {
  margin-right: 16px;
  opacity: 0;
}

.todo-item input:checked + span.check-button::after {
  opacity: 1;
}
</style>
