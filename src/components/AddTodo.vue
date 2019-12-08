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
        ){
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
        submit(e) {
            e.preventDefault();
            const { title } = this.$data;
				this.$apollo.mutate({
					mutation: ADD_TODO,
					variables: {
						title
					},
					refetchQueries: ["getTodos"]
				});
        }
    }
}
</script>