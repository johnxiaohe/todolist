<template>
    <div class="todo">
        <input class="toggle" type="checkbox" @click="checkMethod" :id="todo.id"/>
        <label class="text" :for="todo.id" :style="todo.complete?'text-decoration: line-through; color: slategray;':''">{{ todo.name }}</label>
        <button class="distorybtn" @click="$emit('remove', todo)"><i class="el-icon-delete" /></button>
    </div>
</template>

<script>
import '../assets/todo.css'

export default {
    name: 'Todo',
    props: {
        todo: Object
    },
    methods: {
        checkMethod: function(){
            this.$emit('checkmethod', this.todo)
        }
    }
}
</script>

<style>
.todo {
    width: 100%;
    height: 80px;
    border-top: darkgreen;
    border-top-style: solid;
    /* border-style: solid; */
}

.toggle {
    width: 15%;
    margin-top: 0px;
    display: inline-block;
    vertical-align: top;
}

.text {
    width: 74%;
    box-sizing: border-box;
    display: inline-block;
    line-height: 80px;
    vertical-align: top;
    
}

.distorybtn {
    width: 10%;
    height: 100%;
    font-size: 30px;
    display: inline-block;
    vertical-align: top;
    outline: none;
    border: none;
    background: white;
    cursor: pointer;
}


</style>
