<script setup>
const props = defineProps({
  temp_c:{
  type :Number,
  default: 50
  },
  name:{
  type :String,
  default: "london"
  },
  time:{
  type :String,
  default: "10:10"
  },
  text:{
  type :String,
  default: "sunny"
  },
  icon:{
  type :String,
  default: "sunny"
  }
});
</script>
<template>
  <div class="flex justify-between items-center absolute bottom-16 left-5">
    <div class="flex flex-col mt-10 mx-6">
      <p class="text-9xl text-white font-mono">{{ props.temp_c }}</p>
      <p class="text-5xl mb-5 text-white font-mono">{{ props.name }}</p>
      <p class="text-3xl mb-5 text-white font-mono">{{ props.time }}</p>
      <p class="text-4xl mb-5 text-white font-mono">{{ props.text }}</p>
    </div>
    <!-- <img
      class="object-contain w-20"
      src="../assets/icons8-heavy-rain-50.png"
      alt=""
    /> -->
  </div>
</template>

<style></style>
