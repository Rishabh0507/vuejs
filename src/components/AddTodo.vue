<template>
    <div>
        <form @submit="addtodo">
            <input type="text" v-model="title" name="title" placeholder="Add Todo..">
            <input type="submit" value="submit" class="btn">
        </form>
    </div>
</template>
<script>
//import uuid from 'uuid';
export default {
    name: "AddTodo",
    data (){
        return {
            title: ''
        }
    },
    methods: {
        addtodo(e){
            e.preventDefault();
            // basically we need to construct object so we use const
            // we install uuid for unique value of id and for this we fire npm install uuid command
            const newTodo = {
               // id: uuid.v4(),
                title: this.title,
                completed: false
            }
            //send up to parent
            this.$emit('add-todo',newTodo);
            this.title = '';
        }
    }
}
</script>
<style scoped>
    form {
        display: flex;
    }
    input[type="text"] {
        flex: 10;
        padding: 5px;
    }
    input[type="submit"] {
        flex: 2;
    }
</style>


