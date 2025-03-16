<template>
  <div>
    <todo-input
      v-on:add="addTodo"
    />
    <todo-label
      v-for="todo in sortedTodo"
      v-bind:key="todo.id"
      v-bind:todo="todo"
      v-on:done="doneTodo"
      v-on:remove="removeTodo"
    />
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import { Todo } from '@/types/todo'
import TodoInput from '@/components/TodoInput.vue'
import TodoLabel from '@/components/TodoLabel.vue'

export default Vue.extend({
  components: {
    TodoInput,
    TodoLabel
  },
  data () {
    return {
      todoList: [] as Todo[]
    }
  },
  methods: {
    loadData: async function () {
      // データの読み込み処理
      this.todoList = [] as Todo[]
      console.log('loadData')
    },
    saveData: function () {
      // データの書き込み処理
      console.log('saveData')
    },
    addTodo: function (text: string, color: string) {
      this.todoList = [...this.todoList, {
        id: (new Date()).getTime().toString(),
        done: false,
        date: new Date(),
        text: text,
        color: color
      }]
      this.saveData()
    },
    removeTodo: function (id: string) {
      this.todoList = this.todoList.filter(todo => todo.id !== id)
      this.saveData()
    },
    doneTodo: function (id: string) {
      const todo = this.todoList.find(todo => todo.id === id)
      if (todo) {
        todo.done = !todo.done
        this.saveData()
      }
    }
  },
  computed: {
    sortedTodo (): Todo[] {
      return this.todoList.slice().sort((a, b) => {
        return b.date.getTime() - a.date.getTime()
      })
    }
  },
  beforeCreate () {
    console.log('beforeCreate')
  },
  created () {
    console.log('created')
  },
  beforeMount () {
    console.log('beforeMount')
  },
  async mounted () {
    console.log('mounted')

    // データの読み込み
    await this.loadData()
  },
  beforeUpdate () {
    console.log('beforeUpdate')
  },
  updated () {
    console.log('updated')
  },
  beforeUnmount () {
    console.log('beforeUnmount')
  },
  unmounted () {
    console.log('unmounted')
  }
})
</script>
