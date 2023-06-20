<template>
  <div class="container">
    <div class="row">
      <div class="col-lg-6 offset-lg-3 col-md-8 offset-md-2">
        <div class="input-group mb-3" style="margin-top: 10px;">
          <input
            v-model="data.city"
            @keydown.enter="getWeather"
            class="form-control form-control-lg"
            type="text"
            placeholder="Пошук за містом"
          />
          <button @click="getWeather" class="btn btn-primary btn-lg" type="button">Search</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'WeatherSearch',
  props: {
    data: Object,
    getWeather: Function
  }
};
</script>

<style scoped>
.input-group input {
  border-top-right-radius: 0;
  border-bottom-right-radius: 0;
}

.input-group button {
  border-top-left-radius: 0;
  border-bottom-left-radius: 0;
}
</style>
