<template>
  <h1> Todo List</h1>
  <ul>
    <li v-for="item in TodoItems" :key="item.id">
      <TodoItem :label="item.label" :done="item.done" :id="item.id"></TodoItem>
    </li>
  </ul>
</template>

<script>
import TodoItem from './components/TodoItem.vue'

export default {
  name: 'App',
  components: {
    TodoItem
  },
  data(){
    return {
      TodoItems: [
        {label: 'Learn Vue', done: false, id: 1},
        {label: 'Create a Vue with cli', done: true, id: 2},
        {label: 'Have fun', done: true, id: 3},
        {label: 'Create a todo list', done: false, id:4}
      ]
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
