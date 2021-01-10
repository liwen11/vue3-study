<template>
  <div>
    <button 
      :class="{[$style.active]:currentStatu == item.value}" 
      v-for='(item, index) in status' 
      :key='index'
      @click='changeCurrent(item)'
    >{{item.name}}</button>
  </div>
</template>

<script>
import {reactive, toRefs} from 'vue'
export default {
  props: {
    currentStatu: {
      type: Number,
      required: true
    },
  },
  setup() {
    const status = reactive({
      status: [
        {name: '全部', value: 0},
        {name: '未完成', value: 1},
        {name: '已完成', value: 2},
      ],
    })
    return {...toRefs(status)}
  },
  methods: {
    changeCurrent(item) {
      if (item.value !== this.currentStatu) {
        // this.currentStatu = item.value
        this.$emit('changeCurrent', item.value)
      }
    },
  },
}
</script>

<style module>
.active {
  border-color: red;
}
</style>