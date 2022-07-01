<template>
  <div class="todo-footer">
    <label>
      <input v-model="isAll" type="checkbox">
      <div class="checkmark"></div>
    </label>
    <span>
    <span>已完成 {{ doneTotal }} / 全部 {{ total }}</span>
  </span>
    <button class="btn btn-danger" @click="deleteAll">🗑️</button>
  </div>
</template>

<script>
export default {
  name: "TodoFooter",
  props: ['todos', 'checkAllTodos', 'deleteAllTodo'],
  computed: {
    total() {
      return this.todos.length
    },
    doneTotal() {
      return this.todos.reduce((pre, current) => pre + (current.mode ? 1 : 0), 0);
    },
    isAll: {
      get() {
        return this.doneTotal === this.total && this.total > 0;
      },
      set(value) {
        this.checkAllTodos(value);
        console.log(value);
      }
    }
  },
  methods: {
    deleteAll() {
      this.deleteAllTodo()
    }
  }
}
</script>

<style scoped>
.todo-footer {
  display: flex;
  margin: 24px 2px;
  color: #2f7398;
  font-size: 16px;
  cursor: pointer;
}

/* From uiverse.io by @lenfear23 */
/* Hide the default checkbox */
.container input {
  opacity: 1;
  -webkit-appearance: none;
  cursor: pointer;
  height: 50px;
  width: 50px;
  box-shadow: -10px -10px 15px rgba(255, 255, 255, 0.5),
  10px 10px 15px rgba(0, 0, 70, 0.12);
  border-radius: 50%;
  border: 8px solid #ececec;
  outline: none;
  display: flex;
  justify-content: center;
  align-items: center;
  transition: .5s;
}


.container input::after {
  transition: .5s;
  font-family: monospace;
  content: '';
  color: #7a7a7a;
  font-size: 25px;
  left: 0.45em;
  top: 0.25em;
  width: 0.25em;
  height: 0.5em;
  border: solid #7a7a7a;
  border-width: 0 0.15em 0.15em 0;
  transform: rotate(45deg);
}

.container input:checked {
  box-shadow: -10px -10px 15px rgba(255, 255, 255, 0.5),
  10px 10px 15px rgba(70, 70, 70, 0.12),
  inset -10px -10px 15px rgba(255, 255, 255, 0.5),
  inset 10px 10px 15px rgba(70, 70, 70, 0.12);
  transition: .5s;
}

.container input:checked::after {
  transition: .5s;
  border: solid #15e38a;
  border-width: 0 0.15em 0.15em 0;
  transform: rotate(45deg);
}

span {
  padding: 0 20px 0 20px;
  line-height: 50px;
}

/* From uiverse.io by @adamgiebl */
button {
  position: absolute;
  width: 50px;
  height: 50px;
  right: 30px;
  color: #4592af;
  /*padding: 0.7em 1.7em;*/
  font-size: 17px;
  border-radius: 50%;
  background: #deeaf6;
  border: 8px solid #ececec;
  transition: all .3s;
  box-shadow: 6px 6px 12px #c5c5c5,
  -6px -6px 12px #ffffff;

}

/*button:hover {*/
/*  border: 1px solid white;*/
/*}*/

button:active {
  box-shadow: 4px 4px 12px #c5c5c5,
  -8px -8px 15px #ffffff;
  border: 1px solid white;
}
</style>
