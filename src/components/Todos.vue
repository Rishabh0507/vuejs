<template>
<div>
    <!-- v-for is use as foreach loop to fetch the values from array -->
    <!-- you need to attach a unique key with v-for loop for react -->
    <div v-bind:key="todo.id" v-for="todo in todos">
        <!-- we bind v-for iteration here todo -->
        <!-- now we have to catch v-on:del-todo in app.vue -->
        <TodoItem v-bind:todo="todo" v-on:del-todo="$emit('del-todo',todo.id)" />
    </div>
</div>
</template>
<script>
import TodoItem from './TodoItem.vue';
export default {
    name: "Todos",
    // adding components
    components: {
        TodoItem
    },
    // props is use to accept data from app.vue file
    props: ["todos"]
}
</script>
<style scoped>

</style>


