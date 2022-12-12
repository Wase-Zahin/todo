<template>
  <h1>to do</h1>
  <ToDoForm></ToDoForm>
  <ul>
    <li v-for="item in ToDoItems" :key="item.id">
      <ToDoItemVue 
      :label="item.label" 
      :done="item.done"
      :id="item.id">
    </ToDoItemVue>
    </li>
  </ul>
</template>

<script>
import ToDoForm from './components/ToDoForm';
import ToDoItemVue from './components/ToDoItem.vue';
import uniqueId from 'lodash.uniqueid'

export default {
  name: 'App',
  components: {
    ToDoItemVue,
    ToDoForm
  },
  data() {
    return {
      ToDoItems: [
        { id: uniqueId('todo-'), label: '', done: false }
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
