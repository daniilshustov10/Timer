<template>
    <div class="timer" :class="{active:play}">
        <div class="timer_numbers">
            <div v-if="timer.hours" class="timer-hours">{{hours}}<span class="between-numbers between-numbers__margin">:</span></div>
            <div v-if="timer.hours || timer.minutes" class="timer-minutes">{{minutes}}<span class="between-numbers between-numbers__margin">:</span></div>
            <div class="timer-seconds">{{seconds}}</div>           
        </div>
        <div class="timer-manage">
            <button 
                v-if="play" 
                class='timer-stop' 
                @click="clickStopHandler()"
            >
                <i 
                    class="fa fa-pause" 
                    aria-hidden="true"
                >
                </i>
            </button>
            <button 
                v-else 
                class="timer-play" 
                @click="clickPlayHandler()"
            >
                <i 
                    class="fa fa-play" 
                    aria-hidden="true"
                >
                </i>
            </button>            
            <button 
                class="timer-reset timer-reset__marginLeft" 
                @click="clickResetHandler()"
            >
                <i 
                    class="fa fa-stop" 
                    aria-hidden="true"
                >
                </i>
            </button>
        </div>
    </div>
</template>

<script>
export default {
    props: ['timer'],
    data: () => ({
        play: false,
        interval: null
    }),
    computed: {
        hours() {
            const { hours } = this.timer
            return hours < 10 ? '0' + hours : hours
        },
        minutes() {
            const { minutes } = this.timer
            return minutes < 10 ? '0' + minutes : minutes
        },
        seconds() {
            const { seconds } = this.timer
            return seconds < 10 ? '0' + seconds : seconds
        }
    },
    methods: {
        clickPlayHandler() {
            this.play = true

            this.interval = setInterval(() => {           

                this.timer.seconds++

                if (this.timer.seconds === 60) {
                    this.timer.seconds = 0
                    this.timer.minutes += 1
                }

                if (this.timer.minutes === 60) {
                    this.timer.minutes = 0
                    this.timer.hours += 1
                }

            }, 1000)          
        },
        clickStopHandler() {
            this.play = false
            clearInterval(this.interval)
        },
        clickResetHandler() {
            this.play = false

            if (this.interval) {
                clearInterval(this.interval)
            }

            this.timer.hours = 0
            this.timer.minutes = 0
            this.timer.seconds = 0
        }
    }
}
</script>