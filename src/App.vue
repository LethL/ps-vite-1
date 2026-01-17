<script setup>
    import Button from './components/Button.vue';
    import Score from './components/Score.vue';
    import Card from './components/Card.vue';
    import { ref } from 'vue';

    function handleTurnOverCard(event) {
        console.log(event);
    }

    const score = ref(100);
    const card = ref({
        word: 'dust-coat',
        translation: 'Караван верблюдов',
        state: 'closed',
        status: 'pending'
    })
</script>

<template>
    <header class="header">
        ЗАПОМНИ СЛОВО
        <Score :value="score" /> 
    </header>
    <Card v-bind="card" @turn-over="handleTurnOverCard" />
    <Button />
</template>

<style scoped>
    .header {
        padding: 32px 62px;
        font-weight: 700;
        color: #222222;
        display: flex;
        justify-content: space-between;
    }
</style>
