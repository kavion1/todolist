<template>
		<transition 
        name="animate__animated animate__bouncey" 
        appear
        enter-active-class="animate__slideInDown"
        leave-active-class="animate__slideOutRight"
        >
	<li >
		<label> 
			<input type="checkbox" :checked="todo.done" @change="hanldeid(todo.id)"/>
			<!-- 如下代码也能实现功能，但是不太推荐，因为有点违反原则，因为修改了props -->
			<!-- <input type="checkbox" v-model="todo.done"/> -->
			<span v-show="!todo.isedite">{{todo.title}}</span>
			<input type="text" v-show="todo.isedite" v-model="todo.title" ref="inputupdata" @blur="handleBlur(todo)">
		</label>
		
		<button type="checkbox" class="btn btn-danger" @click="delethanldeid(todo.id)" >删除</button>
		<button type="checkbox" class="btn btn-edite" @click="handleedite(todo)"  v-show="!todo.isedite">编辑</button>
	</li>
	</transition>
</template>

<script>
	import "animate.css"
	export default {
		name:'MyItem',
props:['todo','checkedTodo','deleteTodo'],
methods:{
		hanldeid(a){
			this.checkedTodo(a)
		},
		delethanldeid(id){
			if(confirm('你确定删除吗？')){
				this.deleteTodo(id)
			}
			
		},
	handleedite(todo){
		todo.isedite=!todo.isedite
		this.$nextTick(function(){
			this.$refs.inputupdata.focus()
		})
	
	},
	handleBlur(todo){
		todo.isedite=false
		this.$bus.$on("handleupdata",todo.id,todo.title)
	}
}
	}


</script>

<style scoped>
	/*item*/
	li {
		list-style: none;
		height: 36px;
		line-height: 36px;
		padding: 0 5px;
		border-bottom: 1px solid #ddd;
	}

	li label {
		float: left;
		cursor: pointer;
	}

	li label li input {
		vertical-align: middle;
		margin-right: 6px;
		position: relative;
		top: -1px;
	}

	li button {
		float: right;
		display: none;
		margin-top: 3px;
	}

li:last-child {
		border-bottom: none;
	}

	li:hover{
		background-color: #ddd;
	}
	
	li:hover button{
		display: block;
	}


</style>