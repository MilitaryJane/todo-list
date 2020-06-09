<template>
  <div id="app">
    <h1>Планировщик задач</h1>
    <hr>
    <AddItem />
    <hr>
    <TodoList
      v-bind:todos="todos"
      v-on:remove-item="removeItem"
     />
  </div>
</template>

<script>
import TodoList from '@/components/TodoList'
import AddItem from '@/components/AddItem'
export default {
  name: 'App',
  data() {
		return {
			todos: [
				{id: 1, text: 'Купить шубу', completed: false},
				{id: 2, text: 'Купить сок', completed: false},
				{id: 3, text: 'Купить хлеб', completed: false}
			]
		}
  },
  methods: {
    removeItem(id) {
      this.todos = this.todos.filter(t => t.id !== id)
    }
  },
  components: {
    TodoList, AddItem
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
