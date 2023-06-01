<script setup>
import city from "./city.vue";
import cityShow from "./cityShow.vue";
import cityInfo from "./cityInfo.vue";
import axios from "axios";
import { ref } from "vue";
defineEmits("sendCity");
const citys = ref("");
const cityGet = ref(null);
const allCity = ref([]);
let url = ref("./src/assets/sunny.jpg");
function changBG() {
  if (
    cityGet.value.current.condition.text == "Cloudy" ||
    cityGet.value.current.condition.text == "Partly cloudy"
  ) {
    url.value = "./src/assets/cloudy.jpg";
  } else if (
    cityGet.value.current.condition.text == "Rainy" ||
    cityGet.value.current.condition.text == "Patchy light rain with thunder" ||
    cityGet.value.current.condition.text == "Moderate or heavy rain shower"
  ) {
    url.value = "./src/assets/rainy.jpg";
  } else if (cityGet.value.current.condition.text == "Sunny") {
    url.value = "./src/assets/sunny.jpg";
  } else if (cityGet.value.current.condition.text == "Snowy") {
    url.value = "./src/assets/snowy.jpg";
  } else {
    url.value = "./src/assets/sunny.jpg";
  }
}
function sendCity(n) {
  // debugger;
  this.cityGet.value = this.n;
  console.log(cityGet);
}
function getCity() {
  axios
    .get(
      "http://api.weatherapi.com/v1/current.json?key=2f727a76eebc4c6680374855232805&q=" +
        citys.value +
        "&aqi=yes"
    )
    .then(function (response) {
      cityGet.value = response.data;
      changBG();
      console.log(cityGet);
    })
    .catch(function (error) {
      console.log(error);
    });
  if (citys) {
    this.allCity.push({
      name: this.citys,
    });
    this.citys = "";
  }
  console.log(allCity);
}
</script>

<template>
  <img :src="url" class="absolute w-full h-[100vh]" />
  <div class="flex justify-end container m-auto h-[100vh]">
    <div class="backdrop-blur-xl drop-shadow-xl h-full w-[40%]">
      <div class="flex flex-col h-[100vh] w-full pl-6">
        <!-- search box -->
        <div class="flex flex-col">
          <div class="flex">
            <input
              class="w-full m-2 p-2 bg-inherit outline-none placeholder:font-mono placeholder-gray-800"
              type="text"
              @keyup.enter="getCity()"
              placeholder="Another Location"
              v-model.trim="citys"
            />
            <button @click="getCity()" class="bg-white">
              <img
                class="px-6 my-5"
                src="../assets/icons8-search-30.png"
                alt=""
              />
            </button>
          </div>
          <div class="w-[75%] h-[2px] bg-slate-800 mx-2"></div>
        </div>
        <!-- citys -->
        <city
          @sendCity="'sendCity', sendCity(n)"
          v-for="(city, name, index) in allCity"
          :key="index"
          :name="city.name"
        />
        <div class="flex flex-col">
          <div class="w-[88%] h-[2px] bg-slate-800 mx-2"></div>
        </div>
        <div class="flex flex-col">
          <!-- city show -->
          <cityShow
            v-if="cityGet != null"
            :temp_c="cityGet.current.temp_c"
            :wind_kph="cityGet.current.wind_kph"
            :humidity="cityGet.current.humidity"
            :cloud="cityGet.current.cloud"
          />
          <div class="w-[88%] h-[2px] bg-slate-800 mx-2"></div>
        </div>
      </div>
    </div>
    <!-- city info -->
    <cityInfo
      v-if="cityGet != null"

      :temp_c="cityGet.current.temp_c"
      :name="cityGet.location.name"
      :time="cityGet.location.localtime"
      :text="cityGet.current.condition.text"
      :icon="cityGet.current.condition.icon"
    />
  </div>
</template>
