<template>
	<div>
	<h2>Планировщик задач</h2>
	<hr>
	<router-link to="/">На домашнюю страницу</router-link>
	<hr>
	<AddItem v-on:add-item="addItem"
		/>
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
      this.todos = this.todos.filter(t => t.id !== id);
    },
    addItem(item) {
      this.todos.push(item);
    }
  },
  components: {
    TodoList, AddItem
  }
}
</script>
