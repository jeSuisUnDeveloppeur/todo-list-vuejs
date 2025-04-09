<template>
    <label>
        {{ label }} 
        <input type="checkbox" v-model="model">
    </label>
</template>

<script setup>
    const props = defineProps({
        label:String,
        name:String,
        id:String
    })

    const model = defineModel()
</script>

<style scoped>
</style>