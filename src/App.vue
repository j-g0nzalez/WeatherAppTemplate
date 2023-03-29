<template>
  <section class="highLow" v-if="this.weather.isFahrenheit">
    <h1 class="currentTemp">{{ this.weather.currentTemperature }}°F</h1>
    <h3 class="location">{{ this.weather.location }}</h3>
    <div class="high">High: {{ highTemp }}°F</div>
    <div class="low">Low: {{ lowTemp }}°F</div>
    <div class="hour_frcst"></div>
  </section>
  <section class="highLow" v-else>
    <h1 class="currentTemp">{{ currentCel }}°C</h1>
    <h3 class="location">Long Beach, New Southh Wales, AU</h3>
    <div class="high">High: {{ highCel }}°C</div>
    <div class="low">Low: {{ lowCel }}°C</div>
    <div class="hour_frcst"></div>
  </section>
  <button class="toggle" @click="toggleUnits">
    Toggle Between Celsius/Faranheit
  </button>
</template>

<script>
export default {
  data: function () {
    return {
      weather: {
        location: "Long Beach, CA",
        currentTemperature: 61,
        isFahrenheit: true,
        hourlyForecastToday: [
          59,
          59,
          57,
          57,
          56,
          55,
          54,
          53,
          55,
          57,
          61,
          64,
          68,
          71,
          72,
          71,
          74,
          71,
          70,
          68,
          67,
          64,
          62,
          60,
        ],
      },
    };
  },
  computed: {
    highTemp: function () {
      const tempList = this.weather.hourlyForecastToday;
      return Math.max(...tempList);
    },
    lowTemp: function () {
      const tempList = this.weather.hourlyForecastToday;
      return Math.min(...tempList);
    },
    highCel: function () {
      const faranheit = this.highTemp;
      return (((faranheit - 32) * 5) / 9).toFixed(1);
    },
    lowCel: function () {
      const faranheit = this.lowTemp;
      return (((faranheit - 32) * 5) / 9).toFixed(1);
    },
    currentCel: function () {
      const faranheit = this.weather.currentTemperature;
      return (((faranheit - 32) * 5) / 9).toFixed(1);
    },
  },
  methods: {
    toggleUnits: function () {
      this.weather.isFahrenheit = !this.weather.isFahrenheit;
    },
  },
};
</script>

<style>
#app {
  display: grid;
  grid-template-rows: 1fr 1fr;
  place-items: center;
  height: 100%;
}
.highLow {
  display: grid;
  grid-template-rows: repeat(4, 1fr);
  place-items: center;
  width: 100%;
}
button {
  border-radius: 50px;
  border: 2px solid black;
  background: rgb(79, 137, 245);
  color: #fff;
  padding: 1rem;
  font-size: 1rem;
  height: 20%;
  width: 25%;
  margin: 0 auto;
}
button:hover {
  cursor: pointer;
}
</style>