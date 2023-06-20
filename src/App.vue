<template>
  <div class="gradient-background">
    <div class="container">
      <div class="row">
        <div class="col-lg-10 offset-lg-1 col-md-12">
          <WeatherSearch :data="data" :getWeather="getWeather" />
          <DefaultLocationButton :cityName="data.defaultWeather ? data.defaultWeather.name : ''" :showDefaultWeather="getWeatherByGeolocation" />
          <WeatherDisplay :data="data" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import { reactive, onMounted } from 'vue';
import WeatherSearch from './components/WeatherSearch.vue';
import WeatherDisplay from './components/WeatherDisplay.vue';
import DefaultLocationButton from './components/DefaultLocationButton.vue';

export default {
  name: 'App',
  components: {
    WeatherSearch,
    WeatherDisplay,
    DefaultLocationButton
  },
  setup() {
    let data = reactive({
      city: '',
      currentWeather: null,
      defaultWeather: null
    });

    const apiKey = '562c4dc55ad01e2fc2d559f48dcd11ac';
    const url = 'https://api.openweathermap.org/data/2.5/weather';
    const lang = 'lang=ua';

    const getWeather = async () => {
      if (data.city.trim === '') {
        data.currentWeather = null;
        return;
      }

      try {
        const response = await axios.get(
          `${url}?q=${data.city}&${lang}&units=metric&appid=${apiKey}`
        );
        data.currentWeather = response.data;
      } catch (error) {
        console.error(error);
      }
    };

    const getWeatherByGeolocation = async () => {
      try {
        const position = await new Promise((resolve, reject) => {
          navigator.geolocation.getCurrentPosition(resolve, reject);
        });
        const { latitude, longitude } = position.coords;
        const response = await axios.get(
          `${url}?lat=${latitude}&lon=${longitude}&${lang}&units=metric&appid=${apiKey}`
        );
        data.currentWeather = response.data;
        data.defaultWeather = response.data;
      } catch (error) {
        console.error(error);
      }
    };

    onMounted(getWeatherByGeolocation);

    return { data, getWeather, getWeatherByGeolocation };
  }
};
</script>

<style>
.gradient-background {
  background: linear-gradient(to bottom, #003366, #6699CC);
  height: 100vh;
}
</style>
