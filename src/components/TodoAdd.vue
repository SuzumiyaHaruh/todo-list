<template>
  <div class="input-add">
    <input @keyup.enter="add" v-model="title" type="text" name="text" class="input" style="color: #377ea0"
           placeholder="Type here..."/>
    <button @click="add">+</button>
  </div>
</template>

<script>
import {nanoid} from "nanoid";

export default {
  name: "TodoAdd",
  props: ['addTodo'],
  data() {
    return {
      title: ""
    }
  },
  methods: {
    add() {
      if (this.title === '') {
        this.title = ""
      } else {
        const todo = {id: nanoid(), title: this.title, mode: false}
        this.addTodo(todo)
        this.title = ""
      }

    }
  }
}
</script>

<style scoped>
/* 添加框 */
.input-add {
  position: relative;
  display: flex;
  margin-bottom: 20px;
  align-items: center;
}

.input-add input {
  padding: 16px 52px 16px 18px;
  border: none;
  outline: none;
  width: 100%;
  font-size: 16px;
  background-color: rgb(222, 234, 246);
  box-shadow: rgb(190, 203, 216) 12px 12px 24px 0px inset, rgb(243, 249, 255) -12px -12px 24px 0px inset;
  -webkit-box-shadow: rgb(190, 203, 216) 12px 12px 24px 0px inset, rgb(243, 249, 255) -12px -12px 24px 0px inset;
  border-radius: 40px;
  -webkit-border-radius: 40px;
  transition: 0.3s;

}

.input-add button {
  width: 46px;
  height: 46px;
  font-size: 35px;
  border-radius: 40px;
  background: #4592af;
  border: none;
  color: white;
  position: absolute;
  right: 0px;
  cursor: pointer;
  outline: none;
}

button:hover {
  background: linear-gradient(#226089, #4592af);
}

button:active {
  transform: translateY(-3px);
}
</style>
