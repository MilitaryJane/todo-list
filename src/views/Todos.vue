<template>
  <div>
    <h2>Планировщик задач</h2>
    <hr>
    <router-link to="/">На домашнюю страницу</router-link>
    <hr>
    <AddItem v-on:add-item="addItem"/>
    <hr>
    <select v-model="filter">
      <option value="all">Все задачи</option>
      <option value="completed">Завершенные задачи</option>
      <option value="not-completed">Незавершенные задачи</option>
    </select>
    <hr>
    <TodoList
      v-if="filteredTodos.length"
      v-bind:todos="filteredTodos"
      v-on:remove-item="removeItem"
    />
    <p v-else>Нет задач!</p>
  </div>
</template>

<script>
import TodoList from '@/components/TodoList'
import AddItem from '@/components/AddItem'
export default {
  name: 'App',
  data() {
		return {
      todos: [],
      filter: 'all'
		}
  },
  computed: {
    filteredTodos() {
      if (this.filter === 'all') {
        return this.todos;
      } else if (this.filter === 'completed'){
        return this.todos.filter(t => t.completed);
      } else {
        return this.todos.filter(t => !t.completed);
      }
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
