<template>
  <div>
    <TodoInput 
      v-model="newtodo"
      placeholder="add some todo"
      v-on:keyup.enter='addTodo'
    />
    <Todos
    todopr="some todo"
    second="second"
    :todos="todos"
    @remove="removeTodo"
  />
  </div>
</template>

<script>
import Todos from '@/components/Todos.vue'
import TodoInput from '@/components/TodoInput'
import db from '../../db.json'
import axios from 'axios'

let nextId = 4

export default {
  name: 'todopage',
  components: {
    Todos,
    TodoInput
  },
  data () {
    return {
      todos: null,
      newtodo: ''
    }
  },
  methods: {
    removeTodo (id) {
      console.log(id)
      this.todos = this.todos.filter(item => item.id !== id)
    },
    addTodo () {
      this.todos.push({
        isChecked: false,
        description: this.newtodo.trim(),
        id: nextId++
      })
      this.newtodo = ''
    },
  },
  mounted () {
    // axios
    //   .get(db)
    //   .then(response => this.todos = response.todos)
    //   .catch(error => console.log(error))
    console.log('db', db.todos)
    // fetch(db)
    //   .then(response => response.json())
    //   .then(data => this.todos = data.todos)
    return this.todos = db.todos
  }
}
</script>
