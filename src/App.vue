<template>
   <div class="container">
      <div class="row">
         <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
            <h1 class="text-center">Math Quiz</h1>
         </div>
      </div>
      <hr>
      <div class="row">
         <div class="col-md-3">
            <app-timer
               :newTimer="newTimer"
               @resetTimer="resetTheTimer">
            </app-timer>
         </div>
         <div class="col-xs-12 col-sm-8 col-md-6">
            <transition
               mode="out-in"
               enter-active-class="animated flipInX"
               leave-active-class="animated flipOutX"
               >
               <keep-alive>
                  <component
                     :is="show"
                     @answerCheck="changeComponent"
                     @changeBack="changeToQuestion"
                     :newQuestion="newQuestion">
                  </component>
               </keep-alive>
            </transition>
         </div>
         <div class="col-md-3">
            <app-questiontracker
               :right="right"
               :wrong="wrong"
               >
            </app-questiontracker>
         </div>
      </div>
   </div>
</template>

<script>
import Question from "./components/Question.vue";
import CorrectAnswer from "./components/CorrectAnswer.vue";
import WrongAnswer from "./components/WrongAnswer.vue";
import Timer from "./components/Timer.vue";
import QuestionTracker from "./components/QuestionTracker.vue";

export default {
   data() {
      return {
         show: "app-question",
         newQuestion: 0,
         right: 0,
         wrong: 0,
         newTimer: true
      };
   },
   methods: {
      changeComponent(choice) {
         if (choice) {
            this.show = "app-correct";
            this.newQuestion++;
            this.right++;
         } else {
            this.show = "app-wrong";
            this.newQuestion++;
            this.wrong++;
         }
      },
      changeToQuestion(question) {
         this.show = question;
         this.newTimer = true;
      },
      resetTheTimer() {
         this.newTimer = false;
      }
   },
   components: {
      "app-question": Question,
      "app-correct": CorrectAnswer,
      "app-wrong": WrongAnswer,
      "app-timer": Timer,
      "app-questiontracker": QuestionTracker
   }
};
</script>

<style>

</style>
