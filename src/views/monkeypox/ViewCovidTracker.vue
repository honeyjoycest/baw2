<template>
  <h1 class="text-center mt-4">MonkeyPox Virus Record</h1>
  <h2>
    ID: <span class="text-danger">{{ id }}</span>
  </h2>

  <table class="table table-striped">
    <thead class="bg-primary text-white">
      <tr>
        <th>Coutry</th>
        <th>Deaths</th>
        <th>Recover</th>
        <th>Active Case</th>
        <th>Flag</th>
      </tr>
    </thead>
    <tbody>
      <tr class="hover-list">
        <td>
          {{ covidTracker.country }}
        </td>
        <td>
          {{ covidTracker.deaths }}
        </td>
        <td>
          {{ covidTracker.recovered }}
        </td>
        <td>
          {{ covidTracker.active_case }}
        </td>
        <td>
          <span> <i class="flag flag-france"></i></span>
          <span> <i v-bind:class="{ flag }"></i></span>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  props: ["id"],
  data() {
    return {
      covidTracker: [],
      flag: "ad",
    };
  },

  methods: {
    convertToLowerCase() {},
  },
  mounted() {
    fetch("http://127.0.0.1:8000/api/covid-tracker/" + this.id)
      .then((res) => res.json())
      .then((data) => (this.covidTracker = data))
      .then((res) => console.log(res))
      .catch((err) => console.log(err));
  },
};
</script>

<style>
.width {
  width: 30px;
  height: 30px;
}
.hover-list:hover {
  background: rgb(226, 222, 222);
}
</style>
