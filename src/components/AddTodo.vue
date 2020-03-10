<template>
  <div>
    <form @submit="addTodo">
			<input
				v-model="name" 
				type="text" 
				name="title" 
				placeholder="Add Todo..."
			>
			<input type="submit" value="Submit" class="btn">
		</form>
  </div>
</template>

<script>
import { v4 as uuidv4 } from 'uuid'

export default {
	name:'AddTodo', 
	data(){
		return {
			name:''
		}
	}, 
	methods:{
		addTodo(e){
			e.preventDefault()
			const newTodo = {
				id: uuidv4(), 
				name:this.name, 
				completed:false
			}

			this.$emit('add-todo', newTodo)
			this.name = ''
		}
	}
}
</script>

<style scoped>
	form {
		display: flex;
	}

	input[type="text"]{
		flex: 10;
		padding:5px;
	}
</style>
