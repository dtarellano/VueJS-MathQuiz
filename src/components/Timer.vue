<template>
   <div class="text-center">
      Timer: {{ timer }}
   </div>
</template>

<script>
var time;
export default {
   props: ["newTimer"],
   data() {
      return {
         timer: 10
      };
   },
   methods: {
      stop() {
         if (this.timer === 0) {
            console.log("hi");
            clearInterval(this.setTimer);
         }
      },
      setTimer() {
         time = window.setInterval(() => {
            this.timer--;
         }, 1000);
      }
   },
   created() {
      this.setTimer();
   },
   watch: {
      timer() {
         if (this.timer === 0) {
            window.clearInterval(time);
            // this.$emit("resetTimer");
            // alert("You ran out of time. New Question...");
            this.$emit("timeIsUp", "app-timesup");
         }
      },
      newTimer() {
         if (this.newTimer) {
            console.log("hi");
            window.clearInterval(time);
            this.timer = 10;
            this.setTimer();
            this.$emit("resetTimer");
         }
      }
   }
};
</script>

<style>
</style>
