<template>
   <div class="todo-footer" v-show="todos.length">
            <label>
            <input type="checkbox" v-model="isall" @/>
            </label>
            <span>
            <span>已完成{{doneTotal}}</span> / 全部{{todos.length}}
            </span>
            <button class="btn btn-danger" @click="deleteall">清除已完成任务</button>
        </div>
</template>

<script>
export default {
name:'Myfooter',
props:['todos',"chreckAllTodo",'deleteallTodo'],
computed:{
    doneTotal(){
        let a=0
        this.todos.forEach(element => {
            if(element.done) a++
        })
        return a
    },
    isall:{
        get(){
            return this.doneTotal===this.todos.length && this.todos.length>0;
        },
        set(value){
            this.chreckAllTodo(value);
        }
}
},
methods: {
    deleteall(){
            

            
        if(confirm("您确定要删除所有已完成事项吗"))
            this.deleteallTodo();
            
        
        
    }
},

}
</script>



<style scoped>
	/*footer*/
	.todo-footer {
		height: 40px;
		line-height: 40px;
		padding-left: 6px;
		margin-top: 5px;
	}

	.todo-footer label {
		display: inline-block;
		margin-right: 20px;
		cursor: pointer;
	}

	.todo-footer label input {
		position: relative;
		top: -1px;
		vertical-align: middle;
		margin-right: 5px;
	}

	.todo-footer button {
		float: right;
		margin-top: 5px;
	}
</style>