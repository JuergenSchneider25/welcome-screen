<template>
  <div id="app">
    <h1 class="title">{{ title }}</h1>
    <h2 class="date"> {{currentDate()}} </h2>

    <ul v-if="entries" class="ul">
      <li class="li" v-for="entry in entries" :key="entry.id">
        <span style="color: red">
          {{ entry[0] }} uhr {{ entry[1].replaceAll("/", ".") }}</span
        ><br />
        <span style="color: orange"> {{ entry[2] }}</span> <br />
        <span style="color: orange"> {{ entry[3] }}</span> <br />
      </li>
    </ul>

    <span v-else> No Events! </span>

    <footer class="footer">
      <img class="img-footer" alt="SEB Logo" src="./assets/STZH_SEB_Logo.png" />
      <img
        class="img-footer"
        alt="Opportunity"
        src="./assets/Opportunity.png"
      />
      <img class="img-footer" alt="SAG Logo" src="./assets/SAG_Logo_De.png" />
    </footer>
  </div>
</template>


<script>
import axios from "axios";

export default {
  name: "App",
  data() {
    return {
      title: "Welcome to Opportunity",
      sheet_id: "1a81aI0Y8ViZO0tI92h2YSMqVQJ8hmNNMyMylXgvwiU4",
      api_token: "AIzaSyA-qeDXOhEeQDA0vQf7LgkF7DQtGnAtmAU",
      entries: [],
    };
  },

  computed: {
    gsheet_url() {
      return `https://sheets.googleapis.com/v4/spreadsheets/${this.sheet_id}/values:batchGet?ranges=A2%3AE100&valueRenderOption=FORMATTED_VALUE&key=${this.api_token}`;
    },
  },

  methods: {
    getData() {
      axios.get(this.gsheet_url).then((response) => {
        this.entries = response.data.valueRanges[0].values;
      });
    },

    currentDate() {
      const current = new Date();
      const day = current.getDate();
      const month = current.getMonth() + 1;
      const year = current.getFullYear();
      const dateTime = day + "." + month + "." + year;
      if (month < 10) {
        return day + "." + "0" + month + "." + year;
      }
      return dateTime;
    },

    refreshData() {
      this.currentDate();
      this.getData();
    }
  },

  mounted() {
    this.refreshData();
    setInterval(this.refreshData(), /*1800000000*/);
  },
};
</script>


<style>
body{
  background: #e8e7f3;
}

#app {
  font-family: "Inter", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin-top: 60px;
  color: #393b3d;
}

.title {
  margin-left: 4rem;
  font-size: 4rem;
  margin-bottom: 1rem;
}

.date {
  margin-left: 4rem;
  font-size: 5rem;
  margin-top: 0;
  margin-bottom: 1rem;
  color: #8e8e91;
}


.ul {
  list-style-type: none;
}

.li {
  margin: 60px;
  padding: 3rem;
  background: #0f05a0;
  font-weight: 900;
  font-size: 58px;
  line-height: 86px;
  color: #eb5e00;
}

footer {
  display: flex;
  justify-content: space-between;
  box-sizing: border-box;
  position: fixed;
  bottom: 0px;
  left: 0px;
  width: 100%;
  padding: 40px;
  background: #ffffff;
}

.footer img {
  height: 50px;
}

</style>
