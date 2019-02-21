<template>
  <div>
    <TodoInput
      v-model="newtodo"
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
const todosUrl = 'http://localhost:3000/todos';
const tdUrl = 'http://localhost:3000/';

export default {
  name: "todopage",
  components: {
    Todos,
    TodoInput
  },
  data() {
    return {
      // defaultTodos: null,
      todos: null,
      newtodo: ""
    };
  },
  methods: {
    removeTodo(id) {
      console.log(id);
      // this.todos = this.todos.filter(item => item.id !== id);
      axios
        .delete(`${todosUrl}/${id}`)
        .then(response => console.log(response))
    },
    addTodo() {
      // this.todos.push({
      //   isChecked: false,
      //   description: this.newtodo.trim(),
      //   id: nextId++
      // });
      axios
        .post(todosUrl, {
          isChecked: false,
          description: this.newtodo.trim(),
          id: nextId++
        })
        .then(response => this.todos.push(response.data))
      this.newtodo = "";
    },
    deleteDone() {
      this.todos = this.todos.filter(item => item.isChecked !== true);
      // let result = this.todos.filter(item => item.isChecked !== true);
      // console.log(result)
      // axios
      //   .post(todosUrl, result)
      //   .then(response => this.todos = response.data)
    },
    getData() {
      axios
      .get(todosUrl)
      .then(response => {
        this.todos = response.data;
        // this.defaultTodos = response.data;
        console.log(this.todos)});
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
