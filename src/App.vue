<template>
   <div class="container">
      <div class="row">
         <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
            <h1 class="text-center">Math Quiz</h1>
         </div>
      </div>
      <hr>
      <div class="row">
         <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
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
      </div>
   </div>
</template>

<script>
import Question from "./components/Question.vue";
import CorrectAnswer from "./components/CorrectAnswer.vue";
import WrongAnswer from "./components/WrongAnswer.vue";

export default {
   data() {
      return {
         show: "app-question",
         newQuestion: 0
      };
   },
   methods: {
      changeComponent(choice) {
         if (choice) {
            this.show = "app-correct";
            this.newQuestion++;
         } else {
            this.show = "app-wrong";
         }
      },
      changeToQuestion(question) {
         this.show = question;
      }
   },
   components: {
      "app-question": Question,
      "app-correct": CorrectAnswer,
      "app-wrong": WrongAnswer
   }
};
</script>

<style>

</style>
