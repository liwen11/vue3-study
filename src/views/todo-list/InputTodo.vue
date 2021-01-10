<template>
  <input type="text" :value='inputText' @input="$emit('@update:inputText', $event.target.value)" @keyup.enter="$emit('addTodo', $event)">
</template>
<script>
export default {
  props: {
    inputText: {
      type: String,
      required: true
    },
  },
}
</script>
<style scoped>

</style>