<template>
	<form v-on:submit.prevent="onSubmit"
				v-on:enter="onSubmit">
		<input type="text" v-model="text">
		<button type="submit">Добавить</button>
	</form>
</template>

<script>
export default {
	data() {
		return {
			text: ''
		}
	},
	methods: {
		onSubmit() {
			if (this.text.trim()) {
				const newItem = {
					id: Date.now(),
					text: this.text,
					completed: false
				}
				this.$emit('add-item', newItem);
				this.text = '';
			}
		}
	}
}
</script>

<style scoped>
	form {
		display: flex;
		width: 400px;
		margin: 0 auto;
	}

	input {
		width: 400px;
	}
</style>