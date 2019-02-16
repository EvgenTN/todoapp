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

let nextId = 1

export default {
  name: 'todopage',
  components: {
    Todos,
    TodoInput
  },
  data () {
    return {
      todos: [
        {
          isChecked: false,
          description: 'fgfhhff',
          id: nextId++
        },
        {
          isChecked: true,
          description: '2424242',
          id: nextId++
        },
        {
          isChecked: false,
          description: 'fgfreteyeycmfk fkfkhhff',
          id: nextId++
        }
      ],
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
    }
  }
}
</script>
