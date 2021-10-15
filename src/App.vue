<template>
  <div id="app">
    <h1> Todo List</h1>
    <TodoForm @todo-added="addTodo"></TodoForm>
    <ul>
      <li v-for="item in TodoItems" :key="item.id">
        <TodoItem :label="item.label" :done="item.done" :id="item.id"></TodoItem>
      </li>
    </ul>
  </div>
</template>

<script>
import TodoItem from './components/TodoItem.vue'
import TodoForm from  './components/TodoForm.vue'

export default {
  name: 'App',
  components: {
    TodoItem,
    TodoForm
  },
  data(){
    return {
      TodoItems: [
        {label: 'Learn Vue', done: false, id: "1"},
        {label: 'Create a Vue with cli', done: true, id: "2"},
        {label: 'Have fun', done: true, id: "3"},
        {label: 'Create a todo list', done: false, id:"4"}
      ]
    }
  },
  methods: {
    addTodo(todoLabel){
      console.log('Todo added:', todoLabel)
      this.TodoItems.push({id:"5", label:todoLabel,done:false})
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
