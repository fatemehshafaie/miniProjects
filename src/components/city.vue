<script setup>
import axios from "axios";
import { ref } from "vue"
const emitCity=ref(null)
const props = defineProps({name});
let emit=defineEmits('sendCity')
function changeInfo() {
 emit('sendCity',props.name)
}
</script>
<template>
  <div class="flex flex-col right-0 p-5">
    <a
    @click="changeInfo()"
      class="m-2 cursor-pointer text-xl text-white font-mono hover:text-slate-800 delay-75 transition"
      >{{props.name}}</a>
  </div>
</template>
<style></style>
