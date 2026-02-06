<script setup>
    import Button from './components/Button.vue';
    import Score from './components/Score.vue';
    import Card from './components/Card.vue';
    import { computed, onMounted, ref } from 'vue';

    const score = ref(100);
    const cardsData = ref([]);

    async function getCards() {
        const res = await fetch('http://localhost:8080/api/random-words');
        const data = await res.json();
        cardsData.value = data;
    };

    const dataModify = computed(() => {
        if (cardsData.value.length === 0) {
            return [];
        }
        return cardsData.value.map(card => ({
            ...card,
            state: 'closed',
            status: 'pending'
        }));
    });

    onMounted(() => {
        getCards();
    });
</script>

<template>
    <header class="header">
        ЗАПОМНИ СЛОВО
        <Score :value="score" /> 
    </header>
    <div class="cards">
        <Card v-for="(card, idx) in dataModify" v-bind="card" :key="card.word" :index="++idx" />
    </div>
    <div class="btn_wrapper">
        <Button />
    </div>
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
        flex-wrap: wrap;
        gap: 100px;
        padding: 0 60px;
        margin: 80px 0;
    }

    .btn_wrapper {
        text-align: center;
    }
</style>
