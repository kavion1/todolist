<template>
  <ul class="todo-main">
      <MyItem 
     v-for="todo in fil"
			:key="todo.id" 
			:todo="todo" 
      :checkedTodo='checkedTodo'
      :deleteTodo="deleteTodo"
      />
    </ul>
</template>

<script>
import MyItem from './MyItem.vue'

export default {
		name:'MyList',
		components:{MyItem},
    data() {
      return {
        appsval:''
      }
    },
    props:['todos','checkedTodo','deleteTodo'],
    computed:{
      fil(){
        return  this.todos.filter(todo=>{
                return todo.title.indexOf(this.appsval) !== -1
              
            })
            
      }
    },
    mounted() {
       this.$bus.$on("selecttodo",(sval)=>{
           this.appsval=sval
            
        })
    },
    beforeDestroy() {
      this.$bus.$off("selecttodo")
    },
    

}

</script>

<style scoped>
  
    /*main*/
    .todo-main {
    margin-left: 0px;
    border: 1px solid #ddd;
    border-radius: 2px;
    padding: 0px;
    }

    .todo-empty {
    height: 40px;
    line-height: 40px;
    border: 1px solid #ddd;
    border-radius: 2px;
    padding-left: 5px;
    margin-top: 10px;
    }

</style>