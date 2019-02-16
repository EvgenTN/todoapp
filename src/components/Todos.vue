<template>
  <div class="about">
    <h1>This is todo page</h1>
    <Todo v-for="todo in todos" :key="todo.id" :todo="todo" @remove="removeTodo(todo.id)"
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
    todopr: String,
    second: String,
    todos: Array,
  },
  computed: {},
  methods: {
    removeTodo (id) {
      this.$emit('remove', id)
		}
  }
}
</script>
