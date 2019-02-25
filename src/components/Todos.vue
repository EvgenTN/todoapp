<template>
  <div class="about" v-if='todos'>
    <h1>Todo list:</h1>
    <select :click='getVisibleTodos' v-model="selected">
      <option
        v-for="option in options"
        :key='option.value'
        :value="option.value"
        >{{  option.text }}</option>
    </select>
    <Todo
      v-for="todo in visibleTodos"
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
    todos: Array,
  },
  data() {
    return {
      options: [
        {text: 'all', value: 'all'},
        {text: 'done', value: 'done'},
        {text: 'active', value: 'active'}
      ],
      selected: 'all'
    }
  },
  computed: {
    getVisibleTodos() {
      if (this.todos) {
        this.visibleTodos = this.todos.filter((todo) =>
        (this.selected === 'all') ||
        (todo.isChecked && this.selected === 'done') ||
        (!todo.isChecked && this.selected === 'active'))
      }
    }
  },
  methods: {
    removeTodo (id) {
      this.$emit('remove', id)
    },
    toggleCheck (todo) {
      this.$emit('toggle-check', todo)
    }
  }
}
</script>
