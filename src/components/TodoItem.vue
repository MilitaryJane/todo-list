<template>
	<li>
		<span v-bind:class="{done: item.completed}">
			<input type="checkbox" v-on:change="isComplete">
			<strong>{{ index + 1 }}</strong>
			<span v-if="showEdit"
            v-on:dblclick="toggleShow">
            {{ item.text | uppercase }}
      </span>
      <input class = "edit" type="text"
            v-else
            v-model="item.text"
            v-on:contextmenu.prevent ="toggleShow"
            v-on:keyup.enter="toggleShow">
		</span>
		<button class="remove"
						v-on:click="$emit ('remove-item', item.id)"
		>&times;</button>
	</li>
</template>

<script>
export default {
	data() {
		return {
      showEdit: true
    }
	},
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
    },
    toggleShow() {
      this.showEdit = !this.showEdit;
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

  .edit {
    width: 400px;
  }

</style>
