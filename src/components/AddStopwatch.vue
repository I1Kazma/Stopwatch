<template>
    <div class="add_stopwatch">
        <form @submit.prevent class="add_stopwatch_form">
            <button @click="addStopwatch" class="add_button">+</button>
        </form>
    </div>
</template>

<script>

export default {
    name: 'add-stopwatch',
    data() {
        return {
            stopwatch: {
                id: '',
            }
        }


    },
    methods: {
        addStopwatch(event) {
            this.stopwatch.id = Date.now();
            this.$emit('addStopwatch', this.stopwatch)
        },
    }
}


</script>

<style>
.add_stopwatch {
    height: 120px;
    width: 225px;
    background-color: #696969;
}

.add_stopwatch_form {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 120px;
}

.add_button {
    border: none;
    background-color: #696969;
    color: #9E9E9E;
    width: 40px;
    height: 40px;
    font-size: 37px;
    cursor: pointer;
}
</style>