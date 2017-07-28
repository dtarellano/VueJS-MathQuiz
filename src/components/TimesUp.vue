<template>
   <div class="alert alert-warning text-center" role="alert">
     <h3>Times Up!</h3>
     <button class="btn btn-warning text center" @click="changeBack">New Question</button>
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
