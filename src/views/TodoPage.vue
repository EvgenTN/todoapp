<template>
  <div>
    <TodoInput 
      v-model="newtodo"
      placeholder="add some todo"
    />
    <h2>{{ newtodo }}</h2>
    <Todos
    todopr="some todo"
    second="second"
    :todos="todos"
  />
   <!-- <p v-bind="todos[0].description"></p> -->
  </div>
</template>

<script>
import Todos from '@/components/Todos.vue'
import TodoInput from '@/components/TodoInput'

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
          id: 1
        },
        {
          isChecked: true,
          description: '2424242',
          id: 2
        },
        {
          isChecked: false,
          description: 'fgfreteyeycmfk fkfkhhff',
          id: 3
        }
      ],
      newtodo: ''
    }
  }
}

// const todos = [
//   {
//     isChecked: false,
//     description: "fgfhhff",
//     id: 1
//   },
//   {
//     isChecked: true,
//     description: "2424242",
//     id: 2
//   },
//   {
//     isChecked: false,
//     description: "fgfreteyeycmfk fkfkhhff",
//     id: 3
//   }
// ];
// console.log(todos);
</script>
