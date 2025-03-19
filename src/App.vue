<template>
  <h1 v-if="remainingHours <= 24">The Final Day</h1>
  <h2>- {{ remainingHours }} Hour{{ remainingHours == 1 ? '' : 's' }} Remain -</h2>
</template>

<script>
export default {
  data() {
    return {
      remainingHours: this.calculateRemainingHours(),
    }
  },
  methods: {
    calculateRemainingHours() {
      const now = new Date()
      const theDay = new Date('2025-05-06')

      return Math.floor((theDay - now) / 1000 / 60 / 60)
    },
    updateCountdown() {
      this.remainingHours = this.calculateRemainingHours()
    },
  },
  mounted() {
    this.updateCountdown()
    this.timer = setInterval(this.updateCountdown, 60 * 1000)
  },
  beforeUnmount() {
    clearInterval(this.timer)
  }
}
</script>

<style scoped>
h1 {
  font-size: 7rem;
  margin: 0;
}

h2 {
  font-size: 3rem;
  font-weight: normal;
}
</style>