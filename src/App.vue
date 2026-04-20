<script setup>
    import { ref } from 'vue';

    const count = ref(0)
    const title = "<span>Bienvenue sur le compteur</span>"

    console.log(count, count.value)

    const increment = () => { count.value++}
    const decrement = () => { count.value--}
</script>

<template>
    <h1 v-html="title"></h1>

    <p :style="{ color: count > 5 ?'red' : 'green' }">Compteur : {{ count }}</p>

    <div v-if="count>5">Bravo vous avez cliqué plus de 5 fois</div>
    <div v-else>Vous avez cliqué moins de 5 fois</div>

    <button @click="decrement">Décrémenter</button>
    <button @click="increment">Incrémenter</button>
</template>

<style>
    
</style>