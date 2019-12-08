<template>
    <ul>
        <TodoItem v-for="todo in todos" :key="todo.id" :todo="todo"/>
    </ul>
</template>

<script>
import TodoItem from './TodoItem.vue';

export default {
    name: 'TodoList',
    data() {
        return {
            todos: [
                {
                    id:1,
                    title:'test'
                }
            ]
        } 
    },
    components: {
        TodoItem
    }
}
</script>