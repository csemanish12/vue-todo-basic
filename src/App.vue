<template>
  <div id="app">
    <h1> Todo List</h1>
    <TodoForm @todo-added="addTodo"></TodoForm>
    <h2 id="list-summary" ref="listSummary" tabindex="-1">{{listSummary}}</h2>
    <ul aria-labelledby="list-summary" class="stack-large">
      <li v-for="item in TodoItems" :key="item.id">
        <TodoItem :label="item.label" :done="item.done" :id="item.id" @checkbox-changed="updateDoneStatus(item.id)" @item-deleted="deleteTodo(item.id)" @item-edited="editTodo(item.id, $event)">
        </TodoItem>
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
    },
    updateDoneStatus(todoId){
      const todoUpdate = this.TodoItems.find(item=>item.id === todoId)
      todoUpdate.done = !todoUpdate.done
    },
    deleteTodo(todoId){
      const itemIndex = this.TodoItems.findIndex(item => item.id === todoId)
      this.TodoItems.splice(itemIndex, 1)
      this.$refs.listSummary.focus();
    },
    editTodo(todoId, newLabel){
      const todoToEdit = this.TodoItems.find(item => item.id === todoId)
      todoToEdit.label = newLabel 
    }
  },
  computed: {
    listSummary(){
      const numberFinishedItems = this.TodoItems.filter(item => item.done).length
      return `${numberFinishedItems} out of ${this.TodoItems.length} items completed`
    }
  }
}
</script>

<style>
.btn {
  padding: 0.8rem 1rem 0.7rem;
  border: 0.2rem solid #4d4d4d;
  cursor: pointer;
  text-transform: capitalize;
}
.btn__danger {
  color: #fff;
  background-color: #ca3c3c;
  border-color: #bd2130;
}
.btn__filter {
  border-color: lightgrey;
}
.btn__danger:focus {
  outline-color: #c82333;
}
.btn__primary {
  color: #fff;
  background-color: #000;
}
.btn-group {
  display: flex;
  justify-content: space-between;
}
.btn-group > * {
  flex: 1 1 auto;
}
.btn-group > * + * {
  margin-left: 0.8rem;
}
.label-wrapper {
  margin: 0;
  flex: 0 0 100%;
  text-align: center;
}
[class*="__lg"] {
  display: inline-block;
  width: 100%;
  font-size: 1.9rem;
}
[class*="__lg"]:not(:last-child) {
  margin-bottom: 1rem;
}
@media screen and (min-width: 620px) {
  [class*="__lg"] {
    font-size: 2.4rem;
  }
}
.visually-hidden {
  position: absolute;
  height: 1px;
  width: 1px;
  overflow: hidden;
  clip: rect(1px 1px 1px 1px);
  clip: rect(1px, 1px, 1px, 1px);
  clip-path: rect(1px, 1px, 1px, 1px);
  white-space: nowrap;
}
[class*="stack"] > * {
  margin-top: 0;
  margin-bottom: 0;
}
.stack-small > * + * {
  margin-top: 1.25rem;
}
.stack-large > * + * {
  margin-top: 2.5rem;
}
@media screen and (min-width: 550px) {
  .stack-small > * + * {
    margin-top: 1.4rem;
  }
  .stack-large > * + * {
    margin-top: 2.8rem;
  }
}
/* End global styles */
#app {
  background: #fff;
  margin: 2rem 0 4rem 0;
  padding: 1rem;
  padding-top: 0;
  position: relative;
  box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.2), 0 2.5rem 5rem 0 rgba(0, 0, 0, 0.1);
}
@media screen and (min-width: 550px) {
  #app {
    padding: 4rem;
  }
}
#app > * {
  max-width: 50rem;
  margin-left: auto;
  margin-right: auto;
}
#app > form {
  max-width: 100%;
}
#app h1 {
  display: block;
  min-width: 100%;
  width: 100%;
  text-align: center;
  margin: 0;
  margin-bottom: 1rem;
}
</style>
