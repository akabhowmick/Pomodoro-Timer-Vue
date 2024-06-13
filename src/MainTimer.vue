<!-- html goes here -->

<template>
  <div class="timer">
    <div class="time-display">{{ minutes }}:{{ seconds < 10 ? '0' + seconds : seconds }}</div>
    <div class="controls">
      <!-- onClick => @click -->
      <button @click="startTimer">Start</button>
      <button @click="pauseTimer">Pause</button>
      <button @click="resetTimer">Reset</button>
    </div>
  </div>
</template>

<!-- javascript and functionality come from here: kind of the setup that goes into a react function-->
<script>
export default {
  // variable members
  data() {
    return {
      workDuration: 25 * 60,
      breakDuration: 5 * 60,
      timeLeft: 25 * 60,
      timer: null,
      isRunning: false,
      isWorkSession: true
    }
  },

  computed: {
    minutes() {
      return Math.floor(this.timeLeft / 60)
    },
    seconds() {
      return this.timeLeft % 60
    }
  },

  methods: {
    // button function
    startTimer() {
      if (this.isRunning) return
      this.isRunning = true
      this.timer = setInterval(() => {
        if (this.timeLeft > 0) {
          this.timeLeft--
        } else {
          this.endSession()
        }
      }, 1000)
    },
    // button function
    pauseTimer() {
      this.isRunning = false
      clearInterval(this.timer)
    },
    // button function
    resetTimer() {
      this.isRunning = false
      clearInterval(this.timer)
      this.timeLeft = this.isWorkSession ? this.workDuration : this.breakDuration
    },
    endSession() {
      this.isRunning = false
      clearInterval(this.timer)
      alert(
        this.isWorkSession ? 'Work session ended. Time for a break!' : 'Break ended. Back to work!'
      )
      this.isWorkSession = !this.isWorkSession
      this.timeLeft = this.isWorkSession ? this.workDuration : this.breakDuration
    }
  }
}
</script>

<!-- css goes here -->
<style scoped>
.timer {
  text-align: center;
  font-family: Arial, sans-serif;
}
.time-display {
  font-size: 48px;
  margin-bottom: 20px;
}
.controls button {
  margin: 5px;
  padding: 10px 20px;
  font-size: 16px;
}
</style>
