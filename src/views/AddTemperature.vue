<template>
  <div class="addtemperature">
    <img alt="Medilog logo" src="../assets/Medilog.png" height="180px" width="auto">
    <h3>Sisestage uus kehatemperatuuri mõõtmistulemus</h3>
    <table class="tableTemperature" cellspacing="5">
      <tbody>
<!--      <tr>-->
<!--        <td>Kasutaja ID: </td>-->
<!--        <td><input v-model="addTemperature.userId" placeholder="kustutame, kui login toimib!"></td>-->
<!--        <td></td>-->
<!--      </tr>-->
      <tr>
        <td>Kuupäev: </td>
        <td><input v-model="addTemperature.date" placeholder=""></td>
        <td><i> (aaaa-kk-pp)</i></td>
      </tr>
      <tr>
        <td>Kellaaeg: </td>
        <td><input v-model="addTemperature.time" placeholder=""></td>
        <td><i> (hh:mm)</i></td>
      </tr>
      <tr>
        <td>Kehatemperatuur: </td>
        <td><input v-model="addTemperature.temp" placeholder=""></td>
        <td> °C</td>
      </tr>
      <tr>
        <td>Lisainfo: </td>
        <td><textarea input v-model="addTemperature.addInfo" placeholder="oluline lisateave"></textarea></td>
        <td></td>
      </tr>
      <tr>
        <td></td>
        <button v-on:click="saveInHtml()">Salvesta andmed</button>
        <td></td>
      </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import router from "../router";

let today = new Date();
let dd = String(today.getDate()).padStart(2, '0');
let mm = String(today.getMonth() + 1).padStart(2, '0'); // January is 0
let yyyy = today.getFullYear();
today = yyyy + '-' + mm + '-' + dd;

let now = new Date();
let hours = String(now.getHours()).padStart(2, '0');
let minutes = String(now.getMinutes() + 1).padStart(2, '0');
now = hours + ':' + minutes;

let saveInJs = function () {
  this.$http.post('/medilog/temperature', {},
      {
        params: {
          // userId: this.addTemperature.userId,
          date: this.addTemperature.date,
          time: this.addTemperature.time,
          temp: this.addTemperature.temp,
          addInfo: this.addTemperature.addInfo,
        }
      })
      .then(() => {
        alert('Andmed on salvestatud')
        router.push('/temperatuur')
      })
      .catch(() => alert("Palun täitke kohustuslikud väljad"));
}
export default {
  name: "AddTemperature",
  components: {},
  data: function () {
    return {
      addTemperature: {date :today, time :now}
    }
  },
  methods:
      {
        saveInHtml: saveInJs,
      },
}
</script>

<style scoped>
.tableTemperature {
  text-align: -webkit-center;
  margin-left: auto;
  margin-right: auto;
}
</style>



