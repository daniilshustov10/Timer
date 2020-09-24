<template>
    <div class="timer-list">
        <Timer 
            v-for="timer of timers"
            :timer="timer"
            :key="timer.id"
        />
        <div class="add-timer" @click="$emit('add-timer')">&#10010;</div>
    </div>
</template>

<script>
import Timer from '@/components/Timer'

export default {
    props: ['timers'],
    components: {
        Timer
    }
}
</script>