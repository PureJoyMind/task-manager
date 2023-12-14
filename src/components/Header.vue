<template>
    <header>
        <h1>{{ title }}</h1>
        <Button  color="green" text="Add Task" />
        <!-- <Button color="blue" text="Update Task" />
        <Button color="red" text="Delete Task" /> -->
    </header>
</template>

<script>
import Button from './Button.vue';

export default {
    name: 'Header',
    props:{
        title: {
            type: String,
            default: 'default value of title'
        }
    },
    components:    {
        Button
    }
}
</script>

<style scoped>
    header{
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 20px;
    }
</style>