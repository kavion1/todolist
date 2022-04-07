
<template>
<div id="root" >
    <div class="todo-container">
    <div class="todo-wrap">
<MyHeader />
<!-- @addtodoe="addtodo" -->
<!-- :addTodo="addTodo" -->
<MyList :todos="todos" :checkedTodo="checkedTodo" :deleteTodo="deleteTodo" />
<Myfooter :todos='todos' :deleteallTodo="deleteallTodo" :chreckAllTodo='chreckAllTodo' />
    
</div>
</div>
</div>
</template>
<script>
import MyHeader from './components/MyHeader'
import MyList from './components/MyList'
import Myfooter from './components/Myfooter'
    export default {
        name:"App",
        components:{MyHeader,MyList,Myfooter},
        data() {
            return {
                todos: JSON.parse(localStorage.getItem('todos')) ||[],
                appsval:''
            }
        },
    methods: {
        // addtodo(todoobj){
        //     this.todos.unshift(todoobj)
        // },
        // addTodo(todoObj){
        //     this.todos.unshift(todoObj)
        // },
        checkedTodo(id){
            this.todos.forEach(todo => {
                if(todo.id===id) todo.done=!todo.done
            });
        },
        deleteTodo(id){
            this.todos=this.todos.filter(todo=> todo.id !== id )
        },
        chreckAllTodo(done){
            this.todos.forEach(todo=>todo.done=done)
        },
        deleteallTodo(){
           this.todos=this.todos.filter(todo=>!todo.done)
        },
        hanleupdata(ids,titles){
            this.todos.forEach((todo)=>{
                if(todo.id===ids){
                    todo.title=titles
                }
            })
        }
    },
    mounted(){
            this.$bus.$on("addtodo",(data)=>{
                console.log(data)
            this.todos.unshift(data)
        })
        this.$bus.$on("handleupdata",this.hanleupdata)
       
        
    }
    ,
    befordestroy(){
        this.$bus.$off("addtodo")
    },
    watch:{
      todos:{
				deep:true,
				handler(value){
					localStorage.setItem('todos',JSON.stringify(value))
				}
			},
        chreckAllTodo:{
            deep:true,
            handler(){
                localStorage.setItem(this.todos.done=true)
                console.log(1)
            }

    }
    }}
    </script>
    <style>
    /*base*/
    body {
    background: #fff;
    }

    .btn {
    display: inline-block;
    padding: 4px 12px;
    margin-bottom: 0;
    font-size: 14px;
    line-height: 20px;
    text-align: center;
    vertical-align: middle;
    cursor: pointer;
    box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.05);
    border-radius: 4px;
    }
    .btn-edite{
    color: #fff;
    background-color: aqua;
    border: 1px solid aqua;
    }
    .btn-edite:hover{
    background-color: aqua;
    border: 1px solid rgb(43, 23, 171);
    }
    .btn-danger {
    color: #fff;
    background-color: #da4f49;
    border: 1px solid #bd362f;
    }

    .btn-danger:hover {
    color: #fff;
    background-color: #bd362f;
    }

    .btn:focus {
    outline: none;
    }

    .todo-container {
    width: 800px;
    margin: 0 auto;
    }
    .todo-container .todo-wrap {
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
    }
    </style>