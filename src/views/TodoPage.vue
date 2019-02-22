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
      // this.todos = this.todos.filter(item => item.id !== id);
      return axios
        .delete(`${todosUrl}/${id}`)
        .then(response => console.log(response))
        .then(this.todos = this.todos.filter(item => item.id !== id))
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
          id: this.nextID++
        })
        .then(response => this.todos.push(response.data))
      this.newtodo = "";
    },
    deleteDone() {
      let result = this.todos.filter(item => item.isChecked === true);
      // console.log(result)
      function ad () {for (let todo of result) { axios
        .delete(`${todosUrl}/${todo.id}`)
        .then(response => console.log('answer',response))
        }
      }
      ad()
      this.todos = this.todos.filter(item => item.isChecked !== true);
      // console.log(ad())
      // axios
      //   .delete(`${todosUrl}/${ad().id}`)
      //   .then(response => console.log('answer',response))
        // .then(response => this.todos = response.data)
        // const result = this.todos.filter(item => item.isChecked === true)
        // // console.log(result)
        // return axios
        //   .delete(`${todosUrl}/${id}`, result)
        //   .then(response => console.log('del-done', response))
    },
    getData() {
      return axios
        .get(todosUrl)
        .then(response => {
          this.todos = response.data;
          // this.defaultTodos = response.data;
          console.log(this.todos)});
    },
    toggleCheck(todo) {
      // this.todos = this.todos.map(item => {
      //   if(item.id === todo.id) {
      //     item.isChecked = !item.isChecked
      //   }
      //   return item
      //   })
      todo.isChecked = !todo.isChecked
      return axios
        .patch(`${todosUrl}/${todo.id}`, todo)
        .then(response => console.log(response.data))
    }
  },
  mounted() {
    this.getData()
  },
}
</script>
