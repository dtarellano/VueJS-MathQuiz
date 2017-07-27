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
   mounted() {
      this.setTimer();
   },
   watch: {
      timer() {
         if (this.timer <= 0) {
            window.clearInterval(time);
            if (this.newTimer) {
               this.timer = 10;
               this.setTimer();
               this.$emit("resetTimer");
            }
         }
      }
      // newTimer() {
      //    if (this.newTimer) {
      //       this.timer = 10;
      //       this.setTimer();
      //       this.$emit("resetTimer");
      //    }
      // }
   }
};
</script>

<style>
</style>
