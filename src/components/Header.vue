<template>
    <header>
        <h1>{{ title }}</h1>
        <Button v-show="homepage" @btn-click="$emit('toggle-add-task')" :color="showClose ? 'red' : 'green'" :text="showClose ? 'Close' : 'Add Task'" />
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
        },
        showClose: Boolean
    },
    components:    {
        Button
    },
    computed:{
        homepage(){
            if(this.$route.path === '/') return true;
            return false;
        }
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