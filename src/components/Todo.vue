<template>
  <div class="todo">
    <input id="sss" type="checkbox" checked="isChecked">
    <label for="sss">
      <span>{{ description }} </span>
      <span>{{ isChecked }}</span>
    </label>
  </div>
</template>

<script>
export default {
  name: "Todo",
  props: {
    isChecked: Boolean,
    description: String
  }
};
</script>
<style lang="scss">

</style>
