<template>
    <form @submit="submit">
        <fieldset>
            <input type="text" placeholder="トゥドゥ" v-model="title">
        </fieldset>
        <input class="button-primary" type="submit" value="Send">
    </form>
</template>

<script>
import gql from 'graphql-tag';

// GraphQLクエリを作成します。INSERTなのでmutationです。
// 返り値としてINSERTしたレコードのidを指定しています。
const ADD_TODO = gql`
    mutation addTodo(
        $title: String!
    ) {
        insert_todos(
            objects: [
                {
                    title: $title
                }
            ]
        ) {
            returning {
                id
            }
        }
    }
`;

export default {
    name: "AddTodo",
    data() {
        return {title: ""};
    },
    methods: {
        // submit時にGraphQLでINSERTします。
        submit(e) {
            e.preventDefault();
            const { title } = this.$data;
            // apolloインスタンスを指定してmutateクエリを実行します。
            this.$apollo.mutate({
                mutation: ADD_TODO,
                variables: {
                    title
                },
                // INSERTした後画面をリロードしなくても良いように、TodoListで作ったクエリを自動で実行します。
                refetchQueries: ["getTodos"]
            });
            this.$data.title = "";
        }
    }
}
</script>