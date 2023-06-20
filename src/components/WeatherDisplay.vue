<template>
  <div class="container">
    <div class="row">
      <div class="col-lg-6 offset-lg-3 col-md-8 offset-md-2">
        <div class="card">
          <div class="card-body">
            <div v-if="data.currentWeather">
              <h2 class="card-title">{{ data.currentWeather.name }}</h2>
              <div class="weather-description">
                <h1 class="display-4">{{ Math.round(data.currentWeather.main.temp) }} &#8451;</h1>
                <p class="lead">{{ data.currentWeather.weather[0].description }}</p>
              </div>
              <div class="weather-details">
                <p class="small">Сприйняття температури {{ Math.round(data.currentWeather.main.feels_like) }} &#8451;</p>
                <p class="small">Швидкість вітру {{ data.currentWeather.wind.speed }} м/с</p>
                <p class="small">Вологість {{ data.currentWeather.main.humidity }}%</p>
                <p class="small">Атмосферний тиск {{ (data.currentWeather.main.pressure) * 0.75 }} мм рт.ст.</p>
                <p class="small">Видимість {{ data.currentWeather.visibility }} м</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'WeatherDisplay',
  props: {
    data: Object
  }
};
</script>


<style scoped>
.card-body {
  font-family: sans-serif;
}

.weather-description {
  margin-bottom: 1rem;
}

.weather-details p {
  margin-bottom: 0.5rem;
}

.card-title {
  font-size: 24px;
}
</style>
