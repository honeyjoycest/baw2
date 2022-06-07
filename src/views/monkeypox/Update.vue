<template>
  <h1 class="text-center mt-4">MonkeyPox Virus Record</h1>

  <div class="container w-50 border border-radius p-4">
    <form @submit="postData">
      <div class="form-group">
        <label for="country">Country</label>
        <input
          type="text"
          class="form-control"
          v-model="covidTracker.country"
          id="country"
        />
      </div>
      <div class="form-group">
        <label for="month">Month</label>
        <input
          type="text"
          class="form-control"
          v-model="covidTracker.month"
          id="month"
        />
      </div>
      <div class="form-group">
        <label for="deaths">Deaths</label>
        <input
          type="text"
          class="form-control"
          v-model="covidTracker.deaths"
          id="deaths"
        />
      </div>
      <div class="form-group">
        <label for="recovered">Recovered</label>
        <input
          type="text"
          class="form-control"
          v-model="covidTracker.active_case"
          id="recovered"
        />
      </div>
      <div class="form-group">
        <label for="active_case">Active Case</label>
        <input
          type="text"
          class="form-control"
          v-model="covidTracker.recovered"
          id="active_case"
        />
      </div>

      <button type="submit" class="btn btn-primary mt-4 w-100">Update</button>
    </form>
  </div>
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
    postData(e) {
      e.preventDefault();
      const postData = {
        country: this.covidTracker.country,
        month: this.covidTracker.month,
        deaths: this.covidTracker.deaths,
        active_case: this.covidTracker.active_case,
        recovered: this.covidTracker.recovered,
      };
      console.log("post data");
      console.log(postData);
      console.log("covidtracker");
      console.log(this.covidTracker);

      fetch("http://127.0.0.1:8000/api/covid-tracker/edit/" + this.id, {
        method: "PUT",
        headers: {
          Accept: "application/json",
          "Content-Type": "application/json",
        },
        body: JSON.stringify(postData),
      })
        .then((response) => {
          if (response.status === 200) {
            this.$router.push({ path: "/covid-tracker" });
          }
        })
        .catch((err) => console.log(err));
    },
  },
  mounted() {
    fetch("http://127.0.0.1:8000/api/covid-tracker/" + this.id)
      .then((res) => res.json())
      .then((data) => (this.covidTracker = data))
      .then((res) => {
        console.log("res");
        console.log(res);
      })
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
