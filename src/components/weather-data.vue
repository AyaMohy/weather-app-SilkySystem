<template>
  <div class="full-width weather q-ma-auto">
    <div class="weather__input container">
      <q-input
        standout=" text-lightBlue"
        v-model="cityFeild"
        label="Enter City Name"
        outlined
        @keyup.enter="submit"
      />
    </div>
    <div v-if="weatherInfo">
      <div class="weather__now q-ma-auto flex justify-center items-center">
        <div class="q-pr-md weather__now-text" style="margin: 0">
          {{ weatherInfo.name }}
        </div>
      </div>
      <div class="weather__now q-ma-auto flex justify-center items-center">
        <div class="q-px-sm weather__now-text">
          {{ weatherInfo.weather[0].description }}
        </div>
        <q-icon
          :name="`img:http://openweathermap.org/img/w/${weatherInfo.weather[0].icon}.png`"
          size="lg"
        />
      </div>

      <div
        class="weather__degree q-ma-auto text-center flex justify-center items-center"
      >
        <div>{{ tempDegree }}&deg; {{ temp_unit }}</div>
        <q-btn
          :label="temp_unit == 'C' ? 'Fahrenheit' : 'Celsius '"
          @click="toggleTemp"
          class="weather__degree--btn-toggle"
        />
      </div>
    </div>
  </div>
</template>

<script setup>
import axios from "axios";
import { onBeforeMount, ref } from "vue";
import { useQuasar } from "quasar";
const $q = useQuasar();
const weatherInfo = ref(null);
const tempDegree = ref(null);
const temp_unit = ref("C");
const cityFeild = ref("New Cairo");
const getCurentWeather = async () => {
  try {
    const { data } = await axios.get(
      `http://api.openweathermap.org/geo/1.0/direct?q=${cityFeild.value}&limit=1&appid=078be31b22e6ece778194ba4d21762af`
    );
    const response = await axios.get(`
https://api.openweathermap.org/data/2.5/weather?lat=${data[0]?.lat}&lon=${data[0]?.lon}&units=metric&appid=078be31b22e6ece778194ba4d21762af
`);
    weatherInfo.value = await response.data;
    tempDegree.value = await weatherInfo.value.main.temp;
  } catch (error) {
    // handle error
    $q.dialog({
      title: "Error",
      message:
        "Unable to establish a network connection or incorrect city name entered. Please check your internet connection and ensure the city name is spelled correctly, then try again.",
    }).onOk(() => {
      cityFeild.value = "";
    });
  }
};

// toggle between temperature
const toggleTemp = () => {
  if (temp_unit.value == "C") {
    tempDegree.value = (tempDegree.value * 9) / 5 + 32;
    temp_unit.value = "F";
  } else {
    tempDegree.value = ((tempDegree.value - 32) * 5) / 9;
    temp_unit.value = "C";
  }
};
const submit = () => {
  getCurentWeather();
};
onBeforeMount(() => {
  getCurentWeather();
});
</script>

<style lang="scss" scoped>
.weather {
  margin: 50px auto;
  &__now {
    &-text {
      font-style: normal;
      font-weight: 600;
      font-size: 32px;
      margin: 30px 0;
      color: $primary;
      line-height: 24px;
      @media (max-width: $breakpoint-xs-max) {
        margin: 15px 0;
        font-size: 18px;
      }
    }
  }
  &__degree {
    margin: 20px auto;
    font-style: normal;
    font-weight: 500;
    font-size: 96px;
    line-height: 24px;
    color: #6486ff;
    height: auto;
    height: 67px;
    &--btn-toggle {
      margin-left: 10px;
    }
    @media (max-width: $breakpoint-md-max) {
      font-size: 50px;
    }
    @media (max-width: $breakpoint-xs-max) {
      margin: auto;
      font-size: 32px;
    }
  }
  &__input {
    width: 500px;
    margin: 20px auto;
    @media (max-width: $breakpoint-xs-max) {
      width: 90%;
    }
  }
}
</style>

