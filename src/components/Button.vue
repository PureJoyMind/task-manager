<template>
    <button @click="addTask()" :style="{background: color}" class="btn">{{ text }}</button>
</template>

<script>
export default {
    name: 'Button',
    props:{
        text: String,
        color: String
    },
    methods:{  
        addTask: function () {
            console.log('button');
        }
    }
}
</script>

<style scoped>

</style>