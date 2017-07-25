<template>
   <div class="panel panel-default">
      <div class="panel-heading">
         <h3 class="panel-title text-center">{{ question }}</h3>
      </div>
      <div class="panel-body">
         <div class="col-xs-12 col-sm-6 text-center" v-for="choice in multipleChoice">
            <div class="btn btn-default btn-lg" @click="answerCheck(choice.answer)" style="margin: 5px">
               {{ choice.number}}
            </div>
         </div>
      </div>
   </div>
</template>

<script>
export default {
   props: ["newQuestion"],
   data() {
      return {
         question: "",
         multipleChoice: [
            { answer: false, number: 0 },
            { answer: false, number: 0 },
            { answer: false, number: 0 },
            { answer: false, number: 0 }
         ]
      };
   },
   methods: {
      generateQuestion() {
         const firstNumber = this.numberGenerator(10, 50);
         const secondNumber = this.numberGenerator(10, 50);
         const addOrSubtract = this.numberGenerator(1, 3);
         const rightAnswer = this.numberGenerator(0, 4);
         let correctAnswer = null;

         if (addOrSubtract === 1) {
            correctAnswer = firstNumber + secondNumber;
            this.question = `What is ${firstNumber} + ${secondNumber}?`;
         } else {
            correctAnswer = firstNumber - secondNumber;
            this.question = `What is ${firstNumber} - ${secondNumber}?`;
         }

         // Create Multiple Choice Answers
         this.multipleChoice[0].number = this.numberGenerator(
            correctAnswer - 3,
            correctAnswer + 8,
            correctAnswer
         );
         this.multipleChoice[0].answer = false;
         // Making False when I generate a new question
         this.multipleChoice[1].number = this.numberGenerator(
            correctAnswer - 7,
            correctAnswer + 2,
            correctAnswer
         );
         this.multipleChoice[1].answer = false;
         // Making False when I generate a new question
         this.multipleChoice[2].number = this.numberGenerator(
            correctAnswer - 7,
            correctAnswer + 8,
            correctAnswer
         );
         this.multipleChoice[2].answer = false;
         // Making False when I generate a new question
         this.multipleChoice[3].number = this.numberGenerator(
            correctAnswer - 2,
            correctAnswer + 4,
            correctAnswer
         );
         this.multipleChoice[3].answer = false;
         // Making False when I generate a new question
         // Correct Answer
         this.multipleChoice[rightAnswer].number = correctAnswer;
         this.multipleChoice[rightAnswer].answer = true;
      },

      numberGenerator(min, max, answer) {
         const number = Math.floor(Math.random() * (max - min)) + min;
         if (answer === number) {
            return this.numberGenerator(min, max, answer);
         }
         return number;
      },
      answerCheck(choice) {
         this.$emit("answerCheck", choice);
      }
   },
   created() {
      this.generateQuestion();
   },
   watch: {
      newQuestion() {
         this.generateQuestion();
      }
   }
};
</script>

<style>
</style>
