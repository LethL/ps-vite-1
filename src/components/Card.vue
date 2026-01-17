<script setup>
    const emit = defineEmits(['turn-over', 'change-status']);
    const { word, translation, state, status } = defineProps({
        word: String,
        translation: String,
        state: {
        type: String,
        validator: (value) => ['open', 'closed'].includes(value)
        },
        status: {
        type: String,
        validator: (value) => ['success', 'fail', 'pending'].includes(value)
        },
    });

    function handleTurnOverCard() {
        emit('turn-over', 'Card turned over');
    }
</script>

<template>
    <div class="wrapper">
        <div class="inner">
            <p class="text">01</p>
            <p class="text bottom" @click="handleTurnOverCard()">ПЕРЕВЕНУТЬ</p>
            <p>{{ state === "closed" ? word : translation }}</p>
        </div>
    </div>
</template>

<style scoped>
    .wrapper {
        background-color: #FFFFFF;
        box-shadow: 0px 0px 16px 0px #0000001A;
        border-radius: 16px;
        padding: 28px 19px;
        width: 250px;
        height: 376px;
    }

    .wrapper:hover {
        box-shadow: 0px 0px 16px 0px #00000033;
    }

    .inner {
        border: 1px solid #CCE8FF;
        height: 100%;
        border-radius: 12px;
        position: relative;
        display: grid;
        place-content: center;
    }

    .text {
        position: absolute;
        top: -10px;
        left: 16px;
        margin: 0;
        background-color: #FFFFFF;
    }

    .bottom {
        top: 98%;
        left: 50%;
        transform: translateX(-50%);
    }
</style>
