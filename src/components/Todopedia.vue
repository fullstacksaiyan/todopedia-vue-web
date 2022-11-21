<script setup>
import { ref, computed } from "vue";

const todos = ref([]);
const todo = ref()

const addTodo = () => {
    const newTodo = {
        id: + new Date(),
        description: todo.value,
        completed: false
    }

    todos.value.push(newTodo)

    todo.value = ''
}

const deleteTodo = (id) => {
    const index = todos.value.findIndex(todo => todo.id === id)
    todos.value.splice(index,1)
}

const updateStatusTodo = (id) => {
    const index = todos.value.findIndex(todo => todo.id === id);
    
    todos.value[index].completed = !todos.value[index].completed
}

const pendingTodo = computed(() => todos.value.filter(todo => !todo.completed));

</script>

<template>
    <slot></slot>
    <div class="container">
        <div class="row">
            <div class="offset-md-3 col-md-6">
                <h1 class="text-white text-center my-4">Todopedia</h1>
                <div class="card">
                    <div class="card-body">
                        <form autocomplete="off" v-on:submit.prevent="addTodo">
                            <div class="input-group has-validation">
                                <input type="text" class="form-control" name="descriptions" id="" placeholder="Input Todo" autofocus v-model="todo">
                                <button type="submit" class="btn btn-success">Add</button>
                            </div>
                        </form>
                        <div class="input-group my-3" v-for="todo in todos" :key="todo.id">
                            <label for="" class="form-control" :class="{'text-decoration-line-through': todo.completed}">{{ todo.description }}</label>
                            <button class="btn btn-outline-success" type="button" @click="updateStatusTodo(todo.id)">{{ todo.completed?'Pending':'Complete' }}</button>
                            <button class="btn btn-danger" type="button" @click="deleteTodo(todo.id)">Delete</button>                                
                        </div>
                        <p class="mt-2">You have <strong>{{ pendingTodo.length }}</strong> pending todo</p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>