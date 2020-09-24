<template>
  <div id="app">
    <TimerList 
      :timers="timers"
      @add-timer="addTimer"
    />
  </div>

</template>

<script>
import { v4 as uuidv4 } from 'uuid'
import TimerList from '@/components/TimerList'

export default {
  name: 'App',
  data: () => ({
    timers: [{id: uuidv4(), hours: 0, minutes: 59, seconds: 55}]
  }),
  methods: {
    addTimer() {
      this.timers.push({
        id: uuidv4(), hours: 0, minutes: 0, seconds: 0
      })
    }
  },
  components: {
    TimerList
  }
}
</script>

<style>
  @import './style.css';
</style>


