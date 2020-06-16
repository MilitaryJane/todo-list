<template>
	<li>
		<span v-bind:class="{done: item.completed}">
			<input type="checkbox"
            v-if="showEdit"
            v-on:change="isComplete">
			<strong>{{ index + 1 }}</strong>
			<span v-if="showEdit">
            {{ item.text | uppercase }}
      </span>
      <input class = "edit" type="text"
            v-else
            v-model="item.text"
            v-on:keyup.enter="acceptItem"
            v-on:keyup.esc="cancelEdit">
		</span>
    <div>
      <button class="edit-button"
              v-if="!item.completed && showEdit"
              v-on:click="editItem">
              &#9998;
      </button>
      <button class="accept-button"
              v-else-if="!item.completed && !showEdit"
              v-on:click="acceptItem">
              &#9989;
      </button>
      <button class="remove-button"
              v-on:click="$emit ('remove-item', item.id)">
              &times;
      </button>
    </div>

	</li>
</template>

<script>
export default {
	data() {
		return {
      showEdit: true,
      oldValue: null
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
    isShow() {
      this.showEdit = !this.showEdit;
    },
    editItem() {
      this.isShow();
      this.oldValue = this.item.text;
    },
    acceptItem() {
      this.isShow();
      this.oldValue = null;
    },
    cancelEdit() {
      this.isShow();
      this.item.text = this.oldValue;
      this.oldValue = null;
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

	.remove-button {
		background: red;
		color: #ffffff;
		border-radius: 50%;
		font-weight: 700;
	}

  .edit-button {
		background: yellow;
		color: #000000;
		border-radius: 50%;
		font-weight: 700;
	}
    .accept-button {
		background: green;
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
