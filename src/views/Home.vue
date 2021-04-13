<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <p> {{ diff }} </p>
    <!-- <div v-for="rank in schools"></div>
    <p> {{ rank }} </p> -->
    <p>Name of the school: <input v-model="chosenSchool"> </input></p>
    <button v-on:click="indexSchools">Choose School</button>
    {{ chosenSchool }}
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
      rank: "",
      chosenSchool: 0,
    };
  },
  computed: {
    diff: function () {
      console.log("diff");
      const reading = parseInt(
        this.selected_school.sat_critical_reading_avg_score
      );
      const writing = parseInt(this.selected_school.sat_writing_avg_score);
      const math = parseInt(this.selected_school.sat_math_avg_score);
      return Math.abs((reading + writing) / 2 - math);
    },
  },
  created: function () {
    this.indexSchools();
    this.indexRank();
  },
  methods: {
    indexSchools: function () {
      console.log("getting data...");
      axios
        .get("https://data.cityofnewyork.us/resource/f9bf-2cp4.json")
        .then((response) => {
          console.log(response.data);
          this.schools = response.data;
          this.selected_school = this.schools[`${this.chosenSchool}`];
        });
    },
    indexRank: function () {
      console.log("rank...");
      axios
        .get("https://data.cityofnewyork.us/resource/f9bf-2cp4.json")
        .then((response) => {
          console.log(response.data);
          this.schools = response.data;
          this.selected_school = this.schools[0];
          this.rank = parseInt(this.selected_school.sat_math_avg_score);
        });
    },
  },
};
</script>