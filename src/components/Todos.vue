<template>
    <div class="columns is-multiline">
        <div class="column is-6 is-offset-3">
            <div class="box">
                <form action="#" @submit.prevent=onsubmit>
                    <div class="field">
                        <label class="lable" >Add Your Todo</label>
                        <div class="control">
                            <input class="input" type="text" placeholder="Enter Your Todo..." v-model="title">
                        </div>
                    </div>
                </form>
            </div>
        </div>
        <div class="column is-6 is-offset-3" v-for="todo in todos" :key="todo.id">
            <div class="box todo-box is-flex is-justify-content-space-between is-align-items-center" @click="$emit ('onComplete', todo.id)">
                <span :class="{completed:todo.completed}">{{todo.title}}</span>
                <button class="button is-danger is-small" v-if="todo.completed" @click="$emit('onDelete', todo.id)"> Delete</button>
            </div>
        </div>
    </div>
</template>


<script>
import shortid from 'shortid'
export default {
    name: "Todos",
    props:["todos"],
    data(){
        return{
            title:"",
        };
    },
    methods:{
        onsubmit(){
            const new_todo = {
                title: this.title,
                completed:false,
                id: shortid.generate(),
            };
            this.$emit("addTodo", new_todo);
            this.title ="";
        },
    },
    
};
</script>
<style scoped>
.completed{
    text-decoration: line-through;
}
.todo-box{
    transition: all 0.3s ease;
}
.todo-box:hover{
    cursor: pointer;
    background-color: #f0f3bd;
    transform: scale(1.1);
}
</style>
