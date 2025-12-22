<script setup>
    import Button from './components/Button.vue';
    import Score from './components/Score.vue';
    import Card from './components/Card.vue';

    function handleTurnOverCard(event) {
        console.log(event);
    }
</script>

<template>
    <header class="header">
        ЗАПОМНИ СЛОВО
        <Score value="100" /> 
    </header>
    <Card @turn-over="handleTurnOverCard" />
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
