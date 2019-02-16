<template>
  <div class="todo">
    <input id="todo.id" type="checkbox" :checked="todo.isChecked">
    <label for="todo.id">
      <span>{{ todo.description }} {{todo.id}}</span>
      <!-- <span>{{ todo.isChecked }}</span> -->
    </label>
  </div>
</template>

<script>
export default {
  name: "Todo",
  props: {
    todo: {}
  }
};
</script>
<style lang="scss">

</style>
