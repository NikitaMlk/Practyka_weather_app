<template>

    <div class="container">
        <div class="row">
          <div class="col-lg-6 offset-lg-3 col-md-8 offset-md-2">
            <button type="button" class="btn btn-secondary btn-lg btn-block" @click="showDefaultWeather">
                Локація користувача {{ cityName }}
              </button>
          </div>
        </div>
      </div>

  </template>
  
  <script>
  export default {
    props: {
      cityName: {
        type: String,
        required: true
      },
      showDefaultWeather: {
        type: Function,
        required: true
      }
    }
  };
  </script>
  
  <style scoped>
  .btn-secondary {
    background-color: grey;
    color: white;
    margin-bottom: 1rem;
    font-size: 12px;
    font-weight: bold;
  }
  </style>
  