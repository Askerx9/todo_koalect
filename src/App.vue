<template>
  <div id="app">
    <Todo :list="todoList" @onRemoveEl="handleRemoveElement" @onAddTodo="handleAddElement"/>
  </div>
</template>

<script>
import Todo from './components/Todo.vue'

export default {
  name: 'app',
  components: {
    Todo
  },
  data () {
    return {
      todoList: [
        {
          value: 'Task 1',
          completed: false,
          edit: false
        },
        {
          value: 'Task 2',
          completed: true,
          edit: false
        },
        {
          value: 'Task 3',
          completed: false,
          edit: false
        },
        {
          value: 'Task 4',
          completed: false,
          edit: false
        }
      ]
    }
  },
  methods: {
    /**
     * Add element to list
     */
    handleAddElement () {
      this.todoList.push({
        value: 'New task',
        completed: false,
        edit: true
      })
    },
    /**
     * Remove element
     * @param {int} index - Index of element into array.
     */
    handleRemoveElement (index) {
      this.todoList = this.todoList.filter((el, i) => i !== index)
    }
  }
}
</script>

<style lang="scss">
html,body{
  height: 100%;
  background: #EDF2F7;
}
body{
  font-family: sans-serif;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  color: #3B4958;
}
</style>
