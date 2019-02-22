<template>
  <div class="about">
    <h1>Todo list:</h1>
    <select v-model="changeFilter">
      <option
        v-for="option in options"
        :key='option.value'
        :value="option.value"
        >{{  option.text }}</option>
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
    todos: Array,
  },
  data() {
    return {
      visibleTodos: [],
      filterState: 'all',
      options: [
        {text: 'all', value: 'all'},
        {text: 'done', value: 'done'},
        {text: 'active', value: 'active'}
      ]
    }
  },
  computed: {},
  methods: {
    removeTodo (id) {
      this.$emit('remove', id)
    },
    toggleCheck (todo) {
      this.$emit('toggle-check', todo)
    },
    changeFilter(state) {
    this.filterState = state;
    this.getVisibleTodos();
    },
    getVisibleTodos() {
    if (this.todos) {
      this.visibleTodos = this.todos.filter((todo) =>
       (this.filterState === 'all') ||
        (todo.isChecked && this.filterState === 'done') ||
        (!todo.isChecked && this.filterState === 'active'));
      }
    }
    // getList() {

    // }
  }
}
</script>
