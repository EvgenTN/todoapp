<template>
    <div>
      <input 
      type="text"
      :value="value"
      v-on="listeners"
    />
    <button v-on:click='deleteDone()'>Remove</button>
    </div>
</template>

<script>
export default {
  name: 'TodoInput',
  props: {
    value: {
      type: String,
      default: '',
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
    deleteDone() {
      this.$emit('delDone')
    }
  }
}
</script>
