<template>
    <div>
      <input
      type="text"
      :value="value"
      v-on="listeners"
    />
    <button v-on:click='deleteDone()'>Remove done</button>
    </div>
</template>

<script>
export default {
  name: 'TodoInput',
  props: {
    value: {
      type: String,
      default: ''
    },
    todos: Array
  },
  computed: {
    listeners () {
      return {
        ...this.$listeners,
        input: event => this.$emit('input', event.target.value)
      }
    }
  },
  methods: {
    deleteDone () {
      this.$emit('del-done')
    }
  }
}
</script>

<style lang="scss">
  button {
    border-radius: 5px;
    background: red;
    color: white;
    outline: none;
    border: 0 solid;
    font-size: 16px;
}
</style>
