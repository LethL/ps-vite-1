<script setup>
import { ref, computed } from 'vue';
    const { word, translation, state, status, index } = defineProps({
        word: String,
        translation: String,
        state: {
        type: String,
        validator: (value) => ['open', 'closed'].includes(value)
        },
        status: {
        type: String,
        validator: (value) => ['success', 'fail', 'pending'].includes(value),
        default: 'closed'
        },
        index: Number
    });

    const initialState = ref(state);
    const initialStatus = ref(status);

    function handleTurnOverCard() {
        initialState.value = 'open';
    }

    function handleAnswerCard(status) {
        initialStatus.value = status;
    }

    const dataModify = computed(() => {
        return {
            'isClosed': initialState.value === 'closed',
            'isSuccess': initialStatus.value === 'success',
            'isFail': initialStatus.value === 'fail',
            'isAnswered': initialStatus.value !== 'pending'
        }
    });
</script>

<template>
    <div class="wrapper">
        <div class="inner">
            <p class="text">{{ index }}</p>
            <img v-if="dataModify.isSuccess" src="/assets/yes.svg" alt="success" class="text top" />
            <img v-else-if="dataModify.isFail" src="/assets/no.svg" alt="fail" class="text top" />
            <p>{{ dataModify.isClosed ? word : translation }}</p>
            <p v-if="dataModify.isClosed" class="text bottom" @click="handleTurnOverCard()">ПЕРЕВЕНУТЬ</p>
            <div v-if="!dataModify.isClosed && !dataModify.isAnswered" class="text bottom">
                <img src="/assets/no.svg" alt="no" @click="handleAnswerCard('fail')" />
                <img src="/assets/yes.svg" alt="yes" @click="handleAnswerCard('success')" />
            </div>
            <p v-if="dataModify.isAnswered" class="text bottom">ЗАВЕРШЕНО</p>
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
        padding: 8px;
    }

    .text {
        position: absolute;
        top: -10px;
        left: 16px;
        margin: 0;
        background-color: #FFFFFF;
        cursor: pointer;
    }

    .bottom {
        top: 98%;
        left: 50%;
        transform: translateX(-50%);
        display: flex;
        gap: 32px;
    }

    .top {
        left: 50%;
        transform: translateX(-50%);
        width: 36px;
        height: 36px;
        top: -17px;
    }
</style>
