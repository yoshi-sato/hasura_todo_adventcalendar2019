<template>
    <li :key="todo.id" v-on:click="removeTodo">{{ todo.title }}</li>
</template>

<script>
import gql from 'graphql-tag'

const REMOVE_TODO = gql`
    mutation removeTodo(
        $id: Int!
    ) {
        delete_todos(where: {id: {_eq: $id}}) {
            affected_rows
        }
    }
`;

export default {
    name: "TodoItem",
    props: ["todo"],
    methods: {
        removeTodo() {
            const { id } = this.todo;
            this.$apollo.mutate({
                mutation: REMOVE_TODO,
                variables: {
                    id
                },
                refetchQueries: ["getTodos"]
            });            
        }
    }
}
</script>