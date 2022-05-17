<template>
  <div id="app">
    <h1>Welcome to Opportunity</h1>
    <span> {{ currentDate() }}</span>
    <!-- <span>{{ dateTime() }}</span>  -->
    <p></p>
    <ul>
      <li>
        <!-- <span>08:00 </span> -->
      </li>
    </ul>

    <ul class="ul">
      <li>
        <span style="color: red"> 14:00 Uhr </span> <br />
        <span style="color: orange"> Basisbeschäftigung Besuch</span> <br />
        <span style="color: orange">
          Interessierte für den zweiten Kurs werden uns besuchen</span
        >
      </li>
    </ul>

    <ul class="ul">
      <li>
        <span style="color: red"> 14:00 Uhr </span> <br />
        <span style="color: orange"> Basisbeschäftigung Besuch</span> <br />
        <span style="color: orange">
          Interessierte für den zweiten Kurs werden uns besuchen</span
        >
      </li>
    </ul>

    <ul class="ul">
      <li>
        <span style="color: red"> 14:00 Uhr </span> <br />
        <span style="color: orange"> Basisbeschäftigung Besuch</span> <br />
        <span style="color: orange">
          Interessierte für den zweiten Kurs werden uns besuchen</span
        >
      </li>
    </ul>

    <footer class="footer">
      <img class="img-footer" alt="SEB Logo" src="./assets/STZH_SEB_Logo.png" />
      <img class="img-footer" alt="SAG Logo" src="./assets/SAG_Logo_De.png" />
      <img
        class="img-footer"
        alt="Opportunity"
        src="./assets/Opportunity.png"
      />
    </footer>
  </div>
</template>

<script>
// import axios from "axios";

export default {
  name: "App",
  data() {
    return {
      title: "Welcome to Opportunity",
      sheet_id: "spreadsheets/d/1a81aI0Y8ViZO0tI92h2YSMqVQJ8hmNNMyMylXgvwiU4",
      api_token: "AIzaSyA-qeDXOhEeQDA0vQf7LgkF7DQtGnAtmAU",
    };
  },

  computed: {
    function() {
      return "https://sheets.googleapis.com/v4/spreadsheets/${this.sheet_id}/values:batchGet?ranges=A2%3AE100&valueRenderOption=FORMATTED_VALUE&key=${this.api_token};";
    },
  },

  methods: {
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
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

footer {
  position: fixed;
  display: flex;
  justify-content: space-between;
  box-sizing: border-box;
  left: 0px;
  bottom: 0px;
  width: 100%;
  background: #E8EFF4;
}

.footer img {
  height: 50px;
}

.ul {
  margin-top: 60px;
  margin-bottom: 85px;
  margin-right: 12px;
  margin-left: 10px;
  left: 0px;
  right: 0px;
  top: 70px;
  border-radius: 5px;
  padding: 3rem;
  background: #0f05a0;
}

.li {
  margin-top: 10px;
  margin-bottom: 80px;
  margin-right: 150px;
  margin-left: 20px;
  font-family: "Inter";
  font-style: bold;
  font-weight: 900;
  font-size: 58px;
  line-height: 86px;
  color: #eb5e00;
}
</style>
