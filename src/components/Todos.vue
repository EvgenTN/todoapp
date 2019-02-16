<template>
  <div class="about">
    <h1>This is todo page</h1>
    <!-- <h3>{{ todopr }}</h3> -->
    <!-- <h3>{{ second }}</h3> -->
    <!-- <h3>{{ todos[0].description }}</h3> -->
    <!-- <div v-for="todo in todos" :key="todo.id">{{ todo.description }}</div> -->
    <!-- <pre>{{ todos }}</pre> -->
    <Todo v-for="todo in todos" :key="todo.id" :todo="todo" @remove="removeTodo"
    />
  </div>
</template>

<script>
import Todo from './Todo.vue'
export default {
  name: "Todos",
  components: {
    Todo
  },
  props: {
    todopr: String,
    second: String,
    todos: Array
  },
  // data: {

  // },
  computed: {},
  methods: {}
};
</script>
