<template>
  <div class="other-days flex centered">
    <div v-if="!forecastData" class="flex centered is-black">Loading ...</div>
    <DayForecast
      v-else
      v-for="forecast in dailyForecasts"
      :forecast="forecast"
      :key="forecast.Date"
      :isFahrenheit="isFahrenheit"
    />
  </div>
</template>

<script>
import DayForecast from "@/cmps/DayForecast";
import * as config from "@/services/app.config.json";


export default {
  name: "DayForecastList",
  components: {
    DayForecast
  },
  props: {
    forecastData: {
      type: Object,
      required: true,
      default: () => {},
    },
    city: {
      type: Object,
      required: false,
    },
    isFahrenheit: {
      type: Boolean,
      required: false,
      default: JSON.parse(config.isFahrenheit)
    }
  },
  computed: {
    dailyForecasts() {
      return this.forecastData["DailyForecasts"];
    }
  },
  watch: {
    city: function(val) {
      return val;
    }
  }
};
</script>

<style lang="scss" scoped>
@import "@/assets/css/main.scss";
</style>