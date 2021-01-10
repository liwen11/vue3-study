<template>
  <div>
    <input type="checkbox" :checked='isSelected' @click='$emit("update:isSelected", $event.target.checked)'>
    <span>{{item.content}}</span>
  </div>
</template>

<script>
export default {
  props: {
    item: {
      type: Object,
      required: true
    },
    isSelected: {
      type: Boolean,
      required: true
    },
  },
  methods: {
  },
}
</script>

<style>

</style>