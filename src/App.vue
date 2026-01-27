<script setup>
    import Button from './components/Button.vue';
    import Score from './components/Score.vue';
    import Card from './components/Card.vue';
    import { ref } from 'vue';

    const score = ref(100);
    const data = ref([
        {
        word: 'dust-coat',
        translation: 'Караван верблюдов',
        state: 'closed',
        status: 'pending'
        },        {
        word: 'test',
        translation: 'Караван верблюдов',
        state: 'closed',
        status: 'pending'
        },
    ]);
</script>

<template>
    <header class="header">
        ЗАПОМНИ СЛОВО
        <Score :value="score" /> 
    </header>
    <div class="cards">
        <Card v-for="card in data" v-bind="card" :key="card.word" />
    </div>
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

    .cards {
        display: flex;
        gap: 100px;
        padding: 0 60px;
    }
</style>
