<template>
	<h1>Shopping List</h1>
	<input v-model="input" @keyup.enter="addItem()" /><button @click="addItem()">Add to list</button>
	<h2>Items</h2>
	<ul>
		<li v-for="item in validItems" :key="item.id"><span @click="deleteItem(item)"
				style="margin-right: 15px; cursor: pointer;">X</span><span>{{ item.text }}</span>
		</li>
	</ul>
	<h2>Deleted Items</h2>
	<ul>
		<li v-for="item in deletedItems" :key="item.id"><span @click="eraseItem(item.id)"
				style="margin-right: 15px; cursor: pointer;">X</span><span>{{ item.text }}</span>
		</li>
	</ul>
</template>

<script>
export default {
	data() {
		return {
			input: '',
			list: []
		}
	},
	computed: {
		validItems() {
			return this.list.filter(item => !item.is_deleted)
		},
		deletedItems() {
			return this.list.filter(item => item.is_deleted)
		}
	},
	methods: {
		addItem() {
			this.list.push({
				id: this.list.length + 1,
				text: this.input,
				is_deleted: false
			});
			this.input = ''
		},
		deleteItem(item) {
			item.is_deleted = true
		},
		eraseItem(itemId) {
			const index = this.list.findIndex(item => item.id === itemId)
			if (index !== -1) {
				this.list.splice(index, 1)
			}
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

li span {
	font-size: 1.5em !important;
}

ul {
	padding-left: 0;
	list-style-type: none;
}
</style>
