<template>
   <div class="alert alert-success text-center" role="alert">
     <h3>Correct!</h3>
     <button class="btn btn-success text center" @click="changeBack">New Question</button>
   </div>
</template>

<script>
export default {
   methods: {
      changeBack() {
         this.$emit("changeBack", "app-question");
      }
   }
};
</script>

<style>
</style>
