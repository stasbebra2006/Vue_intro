<template>
	<div class="main">
		<h1>Shopping List</h1>
		<input v-model="newItemName" @keyup.enter="addItem()" />
		<button @click="addItem()">Add to list</button>
		<h2>Items</h2>
		<ul class="item">
			<li v-for="item in validItems" :key="item.id" class="item-text-size">
				<span @click="deleteItem(item)" class="delete-button">X</span>
				<span>{{ item.text }}</span>
			</li>
		</ul>
		<h2>Deleted Items</h2>
		<ul class="item">
			<li v-for="item in deletedItems" :key="item.id" class="item-text-size">
				<span @click="eraseItem(item.id)" class="delete-button">X</span>
				<span>{{ item.text }}</span>
			</li>
		</ul>
	</div>
</template>

<script>
export default {
	data() {
		return {
			newItemName: '',
			itemList: []
		}
	},
	computed: {
		validItems() {
			return this.itemList.filter(item => !item.is_deleted)
		},
		deletedItems() {
			return this.itemList.filter(item => item.is_deleted)
		}
	},
	methods: {
		addItem() {
			if (this.newItemName.trim().length > 0) {
				this.itemList.push({
					id: this.itemList.length + 1,
					text: this.newItemName,
					is_deleted: false
				});
				this.newItemName = ''
			}
		},
		deleteItem(item) {
			item.is_deleted = true
		},
		eraseItem(itemId) {
			const index = this.itemList.findIndex(item => item.id === itemId)
			if (index !== -1) {
				this.itemList.splice(index, 1)
			}
		}
	}
}
</script>

<style>
.main {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	margin-top: 60px;
}

.item-text-size {
	font-size: 1.5em;
}

.item {
	padding-left: 0;
	list-style-type: none;
}

.delete-button {
	margin-right: 15px;
	cursor: pointer;
	color: red;
}
</style>
