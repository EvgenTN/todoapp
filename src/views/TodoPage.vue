<template>
  <div>
    <TodoInput
      v-model="newtodo"
      placeholder="add some todo"
      v-on:keyup.enter="addTodo"
      :todos="todos"
      @delDone="deleteDone"
    />
    <Todos todopr="some todo" second="second" :todos="todos" @remove="removeTodo"/>
  </div>
</template>

<script>
import Todos from "@/components/Todos.vue";
import TodoInput from "@/components/TodoInput";
// import db from "../../db.json";
import axios from "axios";

let nextId = 4;
const todosUrl = 'http://localhost:3000/todos';

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
      this.newtodo = "";
    },
    deleteDone() {
      this.todos = this.todos.filter(item => item.isChecked !== true);
      // const result = this.todos.filter(item => item.isChecked !== true);
      // this.post(result)
    }
  },
  mounted() {
    // axios
    //   .get(this.todosUrl)
    //   .then(response => {this.todos = response});
    fetch(todosUrl)
      .then(response => response.json())
      .then(data => this.todos = data)
  }
};
</script>
