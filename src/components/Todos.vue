<template>
  <div class="about">
    <h1>Todo list:</h1>
    <select>
      <option selected>Show all</option>
      <option>Show done</option>
      <option>Show active</option>
    </select>
    <Todo
      v-for="todo in todos"
      :key="todo.id"
      :todo="todo"
      @remove="removeTodo(todo.id)"
      @toggle-check="toggleCheck(todo)"
    />
  </div>
</template>

<script>
import Todo from './Todo.vue'
export default {
  name: 'Todos',
  components: {
    Todo
  },
  props: {
    todos: Array
  },
  // data() {
  //   return {
  //     tdlist: this.getList()
  //   }
  // },
  computed: {},
  methods: {
    removeTodo (id) {
      this.$emit('remove', id)
    },
    toggleCheck (todo) {
      this.$emit('toggle-check', todo)
    }
    // getList() {

    // }
  }
}
</script>
