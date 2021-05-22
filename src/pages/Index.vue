<template>
  <q-page class="flex column">
    <div class="col q-pt-lg q-px-md">
      <q-input
        @keyup.enter="getWeatherBySearch"
        v-model="search"
        placeholder="Search"
        dark
        borderless
      >
        <template v-slot:before>
          <q-icon @click="getLocation" name="my_location" />
        </template>

        <template v-slot:append>
          <q-btn @click="getWeatherBySearch" round dense flat icon="search" />
        </template>
      </q-input>
    </div>
    <template v-if="wetherData">
      <div class="col text-white text-center">
        <div class="text-h4 text-weight-light">
          {{ wetherData.name }}
        </div>
        <div class="text-h6 text-weight-light">
          {{ wetherData.weather[0].main }}
        </div>
        <div class="text-h1 text-weight-thin q-my-lg relative-position">
          <span>{{ Math.round(wetherData.main.temp) }}</span>
          <span class="text-h4 relative-position degree">&deg;C</span>
        </div>
      </div>

      <div class="col text-center">
        <img
          :src="
            `https://openweathermap.org/img/wn/${wetherData.weather[0].icon}@2x.png`
          "
        />
      </div>
    </template>
    <template v-else>
      <div class="col column text-center text-white">
        <div class="col text-h2 text-weight-thin">Find <br />Weather</div>
        <q-btn @click="getLocation" class="col" flat>
          <q-icon left size="3em" name="my_location" />
          <div>Find My Location</div>
        </q-btn>
      </div>
    </template>

    <div class="skyline"></div>
  </q-page>
</template>

<script>
export default {
  name: "PageIndex",
  data() {
    return {
      search: "",
      wetherData: null,
      lat: null,
      lon: null,
      apiUrl: "https://api.openweathermap.org/data/2.5/weather"
    };
  },
  methods: {
    getLocation() {
      navigator.geolocation.getCurrentPosition(position => {
        this.lat = position.coords.latitude;
        this.lon = position.coords.longitude;
        this.getWeatherByCoords();
      });
    },
    getWeatherByCoords() {
      this.$axios(
        `${this.apiUrl}?lat=${this.lat}&lon=${this.lon}&appid=88ba2bc4848fd043ac403cd03044664d&units=metric`
      ).then(responce => {
        console.log(responce.data);
        this.wetherData = responce.data;
      });
    },
    getWeatherBySearch() {
      this.$axios(
        `${this.apiUrl}?q=${this.search}&appid=88ba2bc4848fd043ac403cd03044664d&units=metric`
      ).then(responce => {
        console.log(responce.data);
        this.wetherData = responce.data;
      });
    }
  }
};
</script>
<style lang="sass">
.q-page
  background: linear-gradient(to top, #74ebd5, #acb6e5)

  .degree
      top: -45px

  .skyline
    flex: 0 0 100px
    background: url(../assets/sky.png)
    background-size: contain
    background-position: center bottom
</style>
