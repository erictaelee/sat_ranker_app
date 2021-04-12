<template>
  <div class="home">
    <h1>{{ message }}</h1>

  </div>
</template>

<style>
</style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
    };
  },
  created: function () {
    this.indexSchools();
  },
  methods: {
    indexSchools: function () {
      console.log("getting data...");
      axios.get("https://data.cityofnewyork.us/resource/f9bf-2cp4.json").then((response) => {
        console.log(response.data);
      });
    },
  },
};
</script>