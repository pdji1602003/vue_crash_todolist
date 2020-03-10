<template>
	<div>
		<div v-for="todo in todos" v-bind:key="todo.id">
			<TodoItem v-bind:todo="todo" v-on:del-todo="$emit('del-todo', todo.id)"/>
		</div>
	</div>
</template>

<script>
import TodoItem from './TodoItem';

export default {
	name:'Todos', 
	components:{
		TodoItem
	},
	props:['todos'] //這個prop是從App.vue傳進來的，傳進來我們就可以開始在目前的component裡使用它
}
</script>

<style scoped>

</style>