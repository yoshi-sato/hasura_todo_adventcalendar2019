<template>
    <ul>
        <TodoItem v-for="todo in todos" :key="todo.id" :todo="todo"/>
    </ul>
</template>

<script>
import TodoItem from './TodoItem.vue';
import gql from 'graphql-tag';

// GETするだけのGrahpQLクエリです。
// idも返すように要求しますが、今回は使っていません。
const GET_TODOS = gql`
    query getTodos {
        todos {
            id
            title
        }
    }
`

export default {
    name: 'TodoList',
    components: {
        TodoItem
    },
    data() {
        return {
            todos: []
        } 
    },
    // apolloで実行するクエリを指定します。
    apollo: {
        todos: {
            query: GET_TODOS
        }
    }
}
</script>