npm<template>
   <div class="todo-header">
       
       <span v-show="selectORadd"> <input type="text" placeholder="请输入你的任务名称，按回车键确认或点击按钮添加" v-model="val" @keyup.enter="addTodos" /></span>
        
        <span v-show="!selectORadd"><input type="text" placeholder="请输入需要查询的任务名称，按回车键确认或点击按钮进行查询" v-model="selectVal" ></span>
        <button @click="change" class="btn">点击{{changebtn}}</button>
      </div>
</template>

<script>
import {nanoid} from 'nanoid'
export default {
    name:"Myfooter",
    data() {
        return {
            val:'',
            selectVal:'',
            selectORadd:true
        }
    },
    computed:{
        changebtn(){
           return  this.selectORadd===true ? "切换为查询":"切换为添加"
        }
    },
    //  props:['addTodo'],
    methods:{
        
        addTodos(){
            if(!this.val) return alert('请输入需要做的事项')
             const todoObj={"id":nanoid(),"title":this.val,"done":false,"isedite":false}
            this.$bus.$emit("addtodo",todoObj)
            this.val=''
        },
        // selects(){
        //     // if(!this.selectVal) return alert('请输入需要查询的内容')
        //     this.$bus.$emit("selecttodo",this.selectVal)
        // },
        change(){
            this.selectORadd=!this.selectORadd
        }
    },
    beforeUpdate() {
        this.$bus.$emit("selecttodo",this.selectVal)
    },
//
//     methods: {
//         addTodos(){
//             if(!this.val) return alert('请输入需要做的事项')
//             const todoObj={"id":nanoid(),"title":this.val,"done":false}
//             this.addTodo(todoObj);
//             this.val=''
//         }
//     }
   
}
</script>

<style scoped>
/*header*/
.btn{
    line-height:26px ;

}
.btn:hover{
    background: rgb(54, 61, 61);
    color: white;
    box-shadow:5px 5px rgba(0, 0, 0, 0.075) ; }
.btn::after{
    background: white;
}
    .todo-header input {
    width: 560px;
    height: 28px;
    font-size: 14px;
    border: 1px solid #ccc;
    border-radius: 4px;
    padding: 4px 7px;
    margin-left:30px ;
    }

    .todo-header input:focus {
    outline: none;
    border-color: rgba(82, 168, 236, 0.8);
    box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 8px rgba(82, 168, 236, 0.6);
    }

</style>