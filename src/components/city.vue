<script setup>
import axios from "axios";
import { ref } from "vue"
const emitCity=ref(null)
const props = defineProps({name});
function changeInfo() {
  // debugger;
  axios
    .get(
      "http://api.weatherapi.com/v1/current.json?key=2f727a76eebc4c6680374855232805&q=" +
       props.name +
        "&aqi=yes"
    )
    .then(function (response) {
      emitCity.value = response.data;
      console.log(emitCity);
    })
    .catch(function (error) {
      console.log(error);
    });
}
</script>
<template>
  <div class="flex flex-col right-0 p-5">
    <a
    @click="changeInfo(),$emit('sendCity',emitCity)"
      class="m-2 cursor-pointer text-xl text-white font-mono hover:text-slate-800 delay-75 transition"
      >{{props.name}}</a>
  </div>
</template>
<style></style>
