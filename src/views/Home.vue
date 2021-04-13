<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <p> {{ diff }} </p>
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
      schools: [],
      selected_school: {},
    };
  },
  computed: {
    diff: function () {
      console.log("diff");
      return Math.abs(
        (this.selected_school.sat_critical_reading_avg_score + this.selected_school.sat_writing_avg_score) / 2 -
          this.selected_school.sat_math_avg_score
      );
    },
  },
  created: function () {
    this.indexSchools();
  },
  methods: {
    indexSchools: function () {
      console.log("getting data...");
      axios.get("https://data.cityofnewyork.us/resource/f9bf-2cp4.json").then((response) => {
        console.log(response.data);
        this.schools = response.data;
        this.selected_school = this.schools[0];
      });
    },
  },
};
</script>