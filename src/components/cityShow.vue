<script setup>
const props = defineProps({
  cloud:{
  type :Number,
  default: 50
  },
  humidity:{
  type :Number,
  default: 50
  },
  wind_kph:{
  type :Number,
  default: 50
  },
  temp_c:{
  type :Number,
  default: 50
  }
});
</script>
<template>
  <div class="flex flex-col right-0 p-5">
    <div class="flex justify-between">
      <p
        class="mx-2 my-5 cursor-pointer text-xl text-white font-semibold font-mono"
      >
        Weather Detail
      </p>
    </div>
    <div class="flex justify-between my-2">
      <p class="m-2 text-xl text-gray-400 font-mono">tempreture</p>
      <p class="m-2 text-xl text-white font-mono">{{ props.temp_c }} C</p>
    </div>
    <div class="flex justify-between my-2">
      <p class="m-2 text-xl text-gray-400 font-mono">wind</p>
      <p class="m-2 text-xl text-white font-mono">{{ props.wind_kph }} km/h</p>
    </div>
    <div class="flex justify-between my-2">
      <p class="m-2 text-xl text-gray-400 font-mono">humidity</p>
      <p class="m-2 text-xl text-white font-mono">{{ props.humidity }} %</p>
    </div>
    <div class="flex justify-between my-2">
      <p class="m-2 text-xl text-gray-400 font-mono">cloud</p>
      <p class="m-2 text-xl text-white font-mono">{{ props.cloud }} %</p>
    </div>
  </div>
</template>

<style></style>
