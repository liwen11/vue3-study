<template>
{{inputText}}
  <input type="text" v-model='inputText' @keyup.enter="addTodo">
  <!-- <InputTodo v-model:inputText='inputText' @addTodo='addTodo'></InputTodo> -->
  <ListItem 
    v-for='(item, index) in realList' 
    :item='item' 
    :key='index'
    v-model:isSelected='item.isCompleted'
  ></ListItem>
  <ChangeTab
    :currentStatu='currentStatu'
    @changeCurrent='changeCurrent'
  ></ChangeTab>
  <span>剩余{{num}}件</span>
  <input type="checkbox" @click='toggelAll($event.target.checked)'>切换
</template> 
<script>
import InputTodo from './InputTodo.vue'
import ListItem from './ListItem.vue'
import ChangeTab from './ChangeTab.vue'

import {reactive, toRefs, computed, watch} from 'vue'
export default {
  components: {
    InputTodo,
    ListItem,
    ChangeTab
  },
  setup() {
    const data = reactive({
      inputText: '现代风格的幸福感'
    })
    const todos = reactive({
      lists: [
        {content: '租的房子地方',  isCompleted: false},
        {content: '租的房子地方2', isCompleted: true},
        {content: '租的房子地方3', isCompleted: true}
      ],
      realList: computed(() => {
        if (tabs.currentStatu === 0) {
          return todos.lists
        } else if (tabs.currentStatu === 1) {
          return todos.lists.filter(val => !val.isCompleted)
        } else {
          return todos.lists.filter(val => val.isCompleted)
        }
      })
    })

    const tabs = reactive({
      currentStatu: 0
    })

    const num = computed(() => {
      return todos.lists.filter(val => !val.isCompleted).length
    })

    return {
      num,
      ...toRefs(data), 
      ...toRefs(todos), 
      ...toRefs(tabs)
    }
  },
  methods: {
    changeCurrent(val) {
      console.log(val)
      this.currentStatu = val
    },
    toggelAll(val) {
      if (val) {
        this.lists = this.lists.map(v => ({...v, isCompleted: true}))
      } else {
        this.lists = this.lists.map(v => ({...v, isCompleted: false}))
      }
    },
    addTodo($event) {
      this.lists.push({
        content: $event.target.value,  isCompleted: false
      })
      this.inputText = ''
    },
  },
}
</script>
<style scoped>

</style>