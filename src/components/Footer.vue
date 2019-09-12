<template>
   <div class="todo-footer">
        <label>
          <input type="checkbox" v-model="checkedAll"/>
        </label>
        <span>
          <span>已完成{{completeNumber}}</span> / 全部{{todos.length}}
        </span>
        <button class="btn btn-danger" v-show="completeNumber" @click="clearFinish">清除已完成任务</button>
      </div>
      
</template>

<script type="text/ecmascript-6">
  export default {
    props:{
      todos:Array,
      selectAll:Function,
      clearFinish:Function
    },
    computed:{
      completeNumber (){
       return this.todos.reduce((pre,item)=>pre+ ( item.finish?1:0),0)
        },
        checkedAll:{
          get (){
            return this.completeNumber===this.todos.length
          },
          set (val){
            this.selectAll(val)
          }
          
        }

      }
    }
  
</script>

<style scoped>
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
