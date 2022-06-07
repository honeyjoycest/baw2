<template>
  <div>
    <hr />
    <div class="container">
      <div class="text-center m-4">
        <h4>MonkeyPox Virus Record</h4>
      </div>
      <div class="container">
        <table class="table table-striped">
          <thead class="bg-primary text-white">
            <tr>
              <th>Country</th>
              <th>Month</th>
              <th>Deaths</th>
              <th>Recovered</th>
              <th>Active Case</th>
              <th class="text-center">Action</th>
            </tr>
          </thead>
          <tbody>
            <tr
              v-for="covid in covidTracker"
              :key="covid.id"
              class="hover-list"
            >
              <td>{{ covid.country }}</td>
              <td>{{ covid.month }}</td>
              <td>{{ covid.deaths }}</td>
              <td>{{ covid.recovered }}</td>
              <td>{{ covid.active_case }}</td>
              <td>
                <router-link
                  :to="{ name: 'view-covid-tracker', params: { id: covid.id } }"
                  class="btn btn-sm btn-success"
                  >open</router-link
                >
                <router-link
                  :to="{
                    name: 'view-covid-tracker-edit',
                    params: { id: covid.id },
                  }"
                  class="btn btn-sm btn-secondary"
                  >Update</router-link
                >
                <router-link
                  :to="{
                    name: 'view-covid-tracker-delete',
                    params: { id: covid.id },
                  }"
                  class="btn btn-sm btn-danger"
                  >Delete</router-link
                >
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      covidTracker: [],
    };
  },
  methods: {
    getData() {
      fetch("http://127.0.0.1:8000/api/covid-tracker/")
        .then((res) => res.json())
        .then((data) => {
          this.covidTracker = data;
        })
        .catch((err) => console.log(err));
    },
  },
  mounted() {
    this.getData();
  },
};
</script>

<style>
.hover-list:hover {
  background: rgb(226, 222, 222);
}
</style>
