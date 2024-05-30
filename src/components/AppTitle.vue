<script setup>
    defineProps({
        title: {
            type:String,
            required: true
        }
    })
</script>

<template>
<div>
    <h1>{{ title }}</h1>
</div>
</template>

<style>
h1{
    color: #5c5c5c;
    display: flex;
    justify-content: center;
    margin: 25px 0 15px;
    font-size: 2rem;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
}

@media (max-width: 900px){
    h1{
        justify-content: center;
        font-size: 1.3rem;
        display: flex;
    }
}
@media (max-width: 900px){
    h1{
        justify-content: center;
        font-size: 1.3rem;
        display: flex;
    }
}
</style>