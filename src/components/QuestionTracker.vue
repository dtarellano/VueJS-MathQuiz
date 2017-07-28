<template>
   <div>
      <div class="text-center">
         How many you got right: {{ right }}
      </div>
      <div class="text-center">
         How many you got wrong: {{ wrong }}
      </div>
  </div>
</template>

<script>
export default {
   props: ["right", "wrong"]
};
</script>

<style>
</style>
