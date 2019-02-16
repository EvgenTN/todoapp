<template>
  <div>
    <Todos 
    todopr="some todo"
    second="second"
    :todos="todos"
  />
   <!-- <p v-bind="todos[0].description"></p> -->
  </div>
</template>

<script>
import Todos from "@/components/Todos.vue";

export default {
  name: "todopage",
  components: {
    Todos
  },
  data () {
    return {
      todos: [
        {
          isChecked: false,
          description: "fgfhhff",
          id: 1
        },
        {
          isChecked: true,
          description: "2424242",
          id: 2
        },
        {
          isChecked: false,
          description: "fgfreteyeycmfk fkfkhhff",
          id: 3
        }
      ]
    };
  }
};

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
