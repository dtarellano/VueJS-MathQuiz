<template>
   <div class="panel panel-default">
      <div class="panel-heading">
         <h3 class="panel-title text-center">{{ question }}</h3>
      </div>
      <div class="panel-body" v-for="choice in multipleChoice">
         {{ choice.number}}
      </div>
   </div>
</template>

<script>
export default {
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
         const addOrSubtract = this.numberGenerator(1, 2);
         const rightAnswer = this.numberGenerator(0, 3);
         let correctAnswer = null;

         if (addOrSubtract === 1) {
            correctAnswer = firstNumber + secondNumber;
            this.question = `What is ${firstNumber} + ${secondNumber}`;
         } else {
            correctAnswer = firstNumber - secondNumber;
            this.question = `What is ${firstNumber} - ${secondNumber}`;
         }

         // Create Multiple Choice Answers
         this.multipleChoice[0].number = this.numberGenerator(
            correctAnswer - 5,
            correctAnswer + 5
         );
         this.multipleChoice[1].number = this.numberGenerator(
            correctAnswer - 5,
            correctAnswer + 5
         );
         this.multipleChoice[2].number = this.numberGenerator(
            correctAnswer - 5,
            correctAnswer + 5
         );
         this.multipleChoice[3].number = this.numberGenerator(
            correctAnswer - 5,
            correctAnswer + 5
         );

         // Correct Answer
         this.multipleChoice[rightAnswer].number = correctAnswer;
         this.multipleChoice[rightAnswer].answer = true;
      },
      numberGenerator(min, max) {
         return Math.floor(Math.random() * (max - min)) + min;
      }
   },
   created() {
      this.generateQuestion();
   }
};
</script>

<style>
</style>
