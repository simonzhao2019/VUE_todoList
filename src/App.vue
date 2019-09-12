<template>
   <div class="todo-container">
    <div class="todo-wrap">
    <Header v-bind:addTodo="addTodo"></Header>
    <List :todos="todos" :removeTodo="removeTodo"></List>
    <Footer :todos="todos" :selectAll="selectAll" :clearFinish="clearFinish"></Footer>
     
     
    </div>
  </div>
</template>
<script type="text/ecmascript-6">
import Header from './components/Header';
import List from './components/List';
import Footer from './components/Footer';
export default {

  data(){
    return {
      todos:[]
    }
  },
  methods:{
    addTodo (todo){
      this.todos.unshift(todo)
    },
    removeTodo (index){
      this.todos.splice(index,1)
    },
    selectAll (checked){
      this.todos.forEach(todo=>todo.finish=checked)
    },
    clearFinish (){
      this.todos=this.todos.filter(todo=>!todo.finish)

    }
  },
  components:{
    Header,
    List,
    Footer
  }
}
</script>

<style scoped>
 .todo-container {
    width: 600px;
    margin: 0 auto;
  }
  .todo-container .todo-wrap {
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
  }
</style>
