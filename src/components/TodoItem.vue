<template>
<!-- now we want to bind is-complete class when task is completed for that we use v-bind:class -->
<!-- if t0d0-completed is true then it binds class is-complete it works like if condition -->
<div class="todo-item" v-bind:class="{'is-complete':todo.completed}">
    <p>
        <input type="checkbox" v-on:change="markComplete">
        {{todo.title}}
        <!-- we can use v-on or @click -->
        <!-- now we catch this id in todo.vue -->
        <button class="del"  @click="$emit('del-todo' , todo.id)">X</button>
        </p>
</div>
</template>
<script>
export default {
    name: "TodoItem",
    // and we use props here for sending data to todos.vue
    props: ["todo"],
    //methods is a object here we define our events
    methods: {
       markComplete(){
           this.todo.completed = !this.todo.completed;
       } 
    }
}
</script>
<style scoped>
.todo-item {
    background: #f4f4f4;
    padding: 10px;
    border-bottom: 1px #ccc dotted;
}
.is-complete{
    text-decoration: line-through;
}
.del{
    background: #ff0000;
    color: #fff;
    border: none;
    padding: 5px 9px;
    border-radius: 50%;
    cursor: pointer;
    float: right;
}
</style>


