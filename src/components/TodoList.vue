<template>
  <div>
    <ul>
      <TodoItem
        v-for="(item, i) in todos"
        v-bind:item="item"
        v-bind:index="i"
        v-bind:key="item.id"
        v-on:remove-item="removeItem"
       />
    </ul>
  </div>
</template>


<script>
import TodoItem from '@/components/TodoItem'
export default {
  props: ['todos'],
  methods: {
    removeItem(id) {
      this.$emit('remove-item', id);
    }
  },
  components: {
    TodoItem
  }
}
</script>

<style scoped>
	ul {
		list-style: none;
		margin: 0;
		padding: 0;
	}
</style>