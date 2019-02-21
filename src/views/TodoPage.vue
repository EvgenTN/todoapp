<template>
  <div>
    <TodoInput
      v-model="newtodo"
      placeholder="add some todo"
      v-on:keyup.enter="addTodo"
      :todos="todos"
      @del-done="deleteDone"
    />
    <Todos :todos="todos" @remove="removeTodo" @toggle-check="toggleCheck"
/>
  </div>
</template>

<script>
import Todos from "@/components/Todos.vue";
import TodoInput from "@/components/TodoInput";
// import db from "../../db.json";
import axios from "axios";

let nextId = 4;
const todosUrl = 'http://localhost:3000/todos/';

export default {
  name: "todopage",
  components: {
    Todos,
    TodoInput
  },
  data() {
    return {
      todos: null,
      newtodo: ""
    };
  },
  methods: {
    removeTodo(id) {
      console.log(id);
      this.todos = this.todos.filter(item => item.id !== id);
    },
    addTodo() {
      this.todos.push({
        isChecked: false,
        description: this.newtodo.trim(),
        id: nextId++
      });
      // axios.post(todosUrl, {
      //   isChecked: false,
      //   description: this.newtodo.trim(),
      //   id: nextId++
      // });
      this.newtodo = "";
    },
    deleteDone() {
      this.todos = this.todos.filter(item => item.isChecked !== true);
      // const result = this.todos.filter(item => item.isChecked !== true);
      // console.log(result)
      // axios.post(todosUrl, result)
    },
    getData() {
      axios
      .get(todosUrl)
      .then(response => {this.todos = response.data; console.log(this.todos)});
    },
    toggleCheck(todo) {
      this.todos = this.todos.map(item => {
        if(item.id === todo.id) {
          item.isChecked = !item.isChecked
        }
        return item
        })
    }
  },
  mounted() {
    this.getData()
  },
}
</script>
