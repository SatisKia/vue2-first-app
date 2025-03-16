<template>
  <div class="label" v-bind:style="{ 'background-color': (todo.done ? '#808080' : todo.color) }">
    <div style="width:100%">
      <table class="table">
        <tbody>
          <tr>
            <td class="td" style="width:5%">
              <input type="checkbox" value="todo.done" v-on:change="done" />
            </td>
            <td class="td" style="width:20%">
              <span>{{ date }}</span>
            </td>
            <td class="td" style="width:65%">
              <span>{{ todo.text }}</span>
            </td>
            <td class="td" style="width:10%">
              <button v-if="todo.done" style="width:100%; border:0" v-bind:style="{ 'background-color': (todo.done ? '#808080' : todo.color) }" v-on:click="remove">消</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script lang="ts">
import Vue, { PropType } from 'vue'
import { Todo } from '@/types/todo'

export default Vue.extend({
  props: {
    todo: {
      type: Object as PropType<Todo>,
      required: true
    }
  },
  methods: {
    done () {
      if (this.$props.todo) {
        this.$emit('done', this.$props.todo.id)
      }
    },
    remove () {
      if (this.$props.todo) {
        this.$emit('remove', this.$props.todo.id)
      }
    }
  },
  computed: {
    date (): string {
      if (!this.$props.todo) return ''
      const { date } = this.$props.todo
      return '' + date.getFullYear() + '年' + (date.getMonth() + 1) + '月' + date.getDate() + '日'
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

<style scoped>
.label {
  margin: 4px 0 0 0;
}
.table {
  border: 0;
}
.td {
  text-align: left;
  vertical-align: middle;
  word-break: break-all;
}
</style>
