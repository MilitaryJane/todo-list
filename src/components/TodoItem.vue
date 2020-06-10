<template>
	<li>
		<span v-bind:class="{done: item.completed}">
			<input type="checkbox" v-on:change="isComplete">
			<strong>{{ index + 1 }}</strong>
			{{ item.text | uppercase }}
		</span>
		<button class="remove"
						v-on:click="$emit ('remove-item', item.id)"
		>&times;</button>
	</li>
</template>

<script>
export default {
	// в props валидируем входящие параметры:
	props: {
		item: {
			type: Object,
			required: true
		},
		index: Number
  },
  filters: {
    uppercase(value){
      return value.toUpperCase()
    }
  },
	methods: {
		isComplete() {
			this.item.completed = !this.item.completed;
		}
	}
}
</script>

<style scoped>
	li {
		border: 1px solid #cccccc;
		display: flex;
		justify-content: space-between;
		padding: 0.5rem 2rem;
		margin-bottom: 1rem;
	}

	.remove {
		background: red;
		color: #ffffff;
		border-radius: 50%;
		font-weight: 700;
	}

	.done {
		text-decoration: line-through;
	}

	input {
		margin-right: 1rem;
	}

</style>
