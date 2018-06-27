<template>
  <view class="container">
    <text class="text-color-primary">{{ text }}</text>
    <button title="天気予報" :on-press="obtainWeather" />
  </view>
</template>
 
<style scoped>
  .container {
    background-color: white;
    align-items: center;
    justify-content: center;
    flex: 1;
  }

  .text-color-primary {
    color: blue;
  }
</style>

<script>
  const CITY_ID = '090010';
  const URL     = `http://weather.livedoor.com/forecast/webservice/json/v1?city=${CITY_ID}`;

  const TODAY    = 0;
  const TOMMOROW = 1;

  export default {
    data() {
      return {
        text: 'My Vue Native App',
      };
    },

    methods: {
      obtainWeather() {
        fetch(URL).then((res) => res.json()).then((e) => {
          const msg = `${e.location.city}の${e.forecasts[TODAY].dateLabel}の天気は...${e.forecasts[TODAY].telop}です！`;
          this.text = msg;
        });
      },
    },
  };
</script>
