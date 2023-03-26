<template>
  <div class="app">
    <div class="app_stopwatch">
      <div class="stopwatches">
        <stopwatch :stopwatches="stopwatches" v-for="stopwatch in stopwatches" />
        <add-stopwatch @addStopwatch="addStopwatch" />
      </div>
    </div>
  </div>
</template>


<script>
import Stopwatch from '@/components/Stopwatch.vue'
import AddStopwatch from '@/components/AddStopwatch.vue'
export default {
  components: { AddStopwatch, Stopwatch },
  data() {
    return {
      stopwatches: [
        { id: 1, },
        { id: 2, },
        { id: 3, },
        { id: 4, },
      ],
    }
  },
  methods: {
    addStopwatch(stopwatch) {
      this.stopwatches.push(stopwatch);
    },
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;

  @font-face {
    font-family: 'Gotham Pro';
    src: url('@/assets/fonts/Gotham/gothampro.ttf');
  }

  font-family: 'Gotham Pro',
  sans-serif;
}

.app {
  background-color: #353638;
  height: 100vh;
}

.app_stopwatch {
  display: Flex;
  align-items: center;
  justify-content: center;
  height: 100vh
}

.stopwatches {
  flex-wrap: wrap;
  width: 775px;
  display: flex;
  flex-direction: row;
  align-items: center;
  gap: 50px;
}

@media (max-width: 774px) {
  .stopwatches {
    width: 500px;
  }
}

@media (max-width:496px) {
  .stopwatches {
    width: 225px;
  }
}
</style>
