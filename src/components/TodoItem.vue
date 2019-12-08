<template>
    <li :key="todo.id">{{ todo.title }}</li>
</template>

<script>
export default {
    name: "TodoItem",
    props: ["todo"]
}
</script>