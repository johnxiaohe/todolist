<template>
  <!-- <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld v-bind:msg="msg"/>
  </div> -->
  <div id="app">
      <span id="title">todos</span>
      <div id="allbox">
        <div id="top">
          <button id="listbtn" @click="btnmethod" ><i :class="[btnSylom]" style="font-size:30px; font-weight:bold; color:#4040448e"></i></button>
          <input placeholder="What needs to be done?" v-model="currentInput" @keyup.enter="createTodo">
        </div>
        <!-- 循环添加子组件 -->
        <div id="todos">
          <Todo v-for="item in showlist" :key="item.id" :todo="item" class="todos-for" @remove="remove" @checkmethod="checkmethod"/>
        </div>
        <div id="follor">
          <span class="follor-num"> {{ todoSum }} items left</span>
            <span class="follor-btn" @click="selectStatus('all')">All</span>
            <span class="follor-btn" @click="selectStatus('active')">Active</span>
            <span class="follor-btn" @click="selectStatus('completed')">Completed</span> 

            <span class="follor-btn" style="float:right" @click="clear">Clear completed</span>
        </div>
      </div>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import './assets/app.css'
import Todo from './components/Todo.vue'

export default {
  name: 'App',
  components: {
    // HelloWorld
    Todo
  },
  data() {
    return {
      currentInput: "",
      index: 0,
      todos: [],
      btnSylom: '',
      currentSelect: 'all'
    }
  },
  computed: {
    todoSum : function(){
      return this.todos.length
    },
    showlist : function(){
      if(this.currentSelect === 'active'){
        return this.todos.filter(i => { return !i.complete; })
      }else if(this.currentSelect === 'completed'){
        return this.todos.filter(i => { return i.complete; })
      }
      return this.todos;
    }
  },
  beforeMount: function() {
    this.btnSylom = 'el-icon-arrow-right'
  },
  methods: {
      createTodo: function(){
        if(!this.currentInput){
          return
        }
        var todo = {
          name: this.currentInput
          ,complete: false
          ,id: this.index
        }
        this.todos.push(todo)
        this.index +=1
        this.currentInput = ""
      },
      btnmethod: function(){
        if(this.btnSylom === 'el-icon-arrow-right'){
          this.btnSylom = "el-icon-arrow-down"
        }else{
          this.btnSylom = "el-icon-arrow-right"
        }
      },
      clear: function(){
        this.todos = this.todos.filter(item =>{
          return !item.complete;
        })
      },
      remove: function(todo){
        this.todos = this.todos.filter(item =>{
          return item.id != todo.id;
        })
      },
      checkmethod: function(todo){
        todo.complete = !todo.complete;
      },
      selectStatus: function(status){
          this.currentSelect = status
      }
  }
}
</script>
