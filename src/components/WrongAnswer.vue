<template>
   <div class="alert alert-danger text-center" role="alert">
     <h3>Wrong!!</h3>
     <button class="btn btn-danger text center" @click="changeBack">New Question</button>
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
