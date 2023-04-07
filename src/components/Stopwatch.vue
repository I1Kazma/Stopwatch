<template>
    <div class="stopwatch">

        <div class="time">
            <span class="time_info" :style="UIStyle">{{ time }}</span>
        </div>

        <div class="line" :style="lineStyle"></div>

        <div class="buttons">
            <span class="button_start" :style="UIStyle" @click="StopwatchStart()" v-if="isStopwatchStop">▶</span>
            <div class="buttons_pause" v-if="isStopwatchStart" @click="StopwatchPause()">
                <span class="button_pause" :style="lineStyle">
                </span>
                <span class="button_pause" :style="lineStyle">
                </span>
            </div>
            <span class="button_stop" :style="UIStyle" @click="StopwatchReset()">&#9632;</span>
        </div>

    </div>
</template>

<script>
export default {
    name: 'stopwatch',
    props: {
        stopwatches: {
            type: Array,
            required: true,
        }
    },

    data() {
        return {
            timer: null,
            time: '00:00:00',
            seconds: 0,
            minutes: 0,
            hours: 0,
            showMinutes: false,
            showHours: false,
            lineStyle: {
                background: '#9E9E9E'
            },
            UIStyle: {
                color: '#9E9E9E'
            },
            isStopwatchStart: false,
            isStopwatchStop: true,
        }
    },
    methods: {

        StopwatchStart() {
            this.startTime = performance.now();
            this.isStopwatchStart = true;
            this.isStopwatchStop = false;
            this.UIStyle.color = 'white';
            this.lineStyle.background = 'white';
            this.updateStopwatch();
        },
        updateStopwatch() {
            this.timer = requestAnimationFrame(() => {
                const elapsed = performance.now() - this.startTime;
                const seconds = Math.floor(elapsed / 1000);
                const minutes = Math.floor(seconds / 60);
                const hours = Math.floor(minutes / 60);

                this.seconds = seconds % 60;
                this.minutes = minutes % 60;
                this.hours = hours;

                this.time =
                    (this.hours > 9 ? this.hours : '0' + this.hours) + ':' +
                    (this.minutes > 9 ? this.minutes : '0' + this.minutes) + ':' +
                    (this.seconds > 9 ? this.seconds : '0' + this.seconds);

                if (this.isStopwatchStart) {
                    this.updateStopwatch();
                }
            });
        },
        StopwatchPause() {
            cancelAnimationFrame(this.timer);
            this.UIStyle.color = '#9E9E9E';
            this.lineStyle.background = '#9E9E9E';
            this.isStopwatchStart = false;
            this.isStopwatchStop = true;
        },
        StopwatchReset() {
            this.seconds = 0
            this.minutes = 0
            this.hours = 0
            this.time = '00:00:00'
            this.showMinutes = false
            this.showHours = false
            this.UIStyle.color = '#9E9E9E';
            this.lineStyle.background = '#9E9E9E';
            cancelAnimationFrame(this.timer);
            this.isStopwatchStart = false;
            this.isStopwatchStop = true;
        },


    }
}
</script>

<style>
.stopwatch {
    height: 120px;
    width: 225px;
    background-color: #696969;
}

.line {
    height: 1px;
    width: 100%;
    background: #9E9E9E;
}

.time {
    height: 60px;
    display: flex;
    justify-content: center;
    align-items: center;
}

.time_info {
    font-size: 22px;
    line-height: 21px;
}

.buttons {
    height: 60px;
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 48px;
}

.button_start {
    padding-top: 1px;
    width: 17px;
    font-size: 25px;
    cursor: pointer;
}

.buttons_pause {
    display: flex;
    width: 17px;
    height: 20px;
    align-items: center;
    justify-content: center;
    gap: 4px;
    cursor: pointer;
}

.button_pause {
    width: 3px;
    height: 20px;
}

.button_stop {
    height: 60px;
    width: 20px;
    font-size: 42px;
    cursor: pointer;
}
</style>
