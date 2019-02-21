<template>
  <div class="todo">
    <input
      :id="todo.id"
      type="checkbox"
      :checked="todo.isChecked"
      v-on:click='$emit("toggle-check", todo)'
      >
    <label :for="todo.id">
      <span>{{ todo.description }}</span>
    </label>
    <button v-on:click='$emit("remove", todo.id)'>DLT</button>
  </div>
</template>

<script>
export default {
  name: 'Todo',
  props: {
    todo: {}
  }
}
</script>

<style lang="scss">
.todo {
  display: flex;
  align-items: center;
  position: relative;
  text-align: start;
  width: 100%;
  margin-bottom: 15px;
  label {
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
      padding-left: 15px;
      padding-right: 40px;
  }
  input:checked + label {
    color: rgb(196, 196, 196);
  }
  button {
    position: absolute;
    right: 0;
    color: white;
    background: red;
    border: 0 solid;
    outline: none;
    border-radius: 50%;
    padding: 5px;
  }
}
</style>
