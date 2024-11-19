<script>
import axios from 'axios'
export default {
  data() {
    return {
      city: "",
      error: "",
      info: null
    }
  },
  computed: {
    cityName() {
      return this.city
    },
    showTemp(){
      return "Temperature: " + this.info.main.temp + " °F"
    },
    showFeelsLike(){
      return "Feels like: " + this.info.main.feels_like + " °F"
    },
    showMinTemp(){
      return "Min temperature: " + this.info.main.temp_min + " °F"
    },
    showMaxTemp(){
      return "Max temperature: " + this.info.main.temp_max + " °F"
    },
  },
  methods: {
    getWeather() {
      if(this.city.trim().length < 2) {
        this.error = "Please enter more than one symbol"
        return false
      }
      this.error=""

      axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&appid=d8c6b5d5c56020ac63f75e8907d9f222`)
      .then(res => (this.info = res.data))
  }
  }
}
</script>

<template>
  <div class="wrapper">
    <h1>What the weather?</h1>
    <p>{{ city == "" ? "Your city" : cityName}}</p>
    <input type="text" v-model="city" placeholder="Enter city">
    <button v-show="city !=''" @click="getWeather()">Get</button>
    <p class="error">{{ error }}</p>
    <div v-if="info != null">
      <p>{{ showTemp }}</p>
      <p>{{ showFeelsLike }}</p>
      <p>{{ showMinTemp }}</p>
      <p>{{ showMaxTemp }}</p>
    </div>
  </div>
</template>

<style scoped>

.error{
  color: red;
}
.wrapper {
  width: 800px;
  height: 400px;
  border-radius: 50px;
  padding: 20px;
  text-align: center;
  font-family: Arial, Helvetica, sans-serif;
  background-color: rgba(240, 248, 255, 0.295);
}
.wrapper h1{
  margin-top: 50px;
}
.wrapper p {
  margin-top: 20px;
}

.wrapper input {
  margin-top: 30px;
  background: transparent;
  border: 0;
  border-bottom:  2px solid black;
  font-size: 14px;
  padding: 5px 8px;
  outline: none;
}

.wrapper input:focus {
  border-bottom-color: aliceblue;
}

.wrapper button {
  background: #fff;
  border-radius: 10px;
  padding: 10px 15px;
  margin-left: 20px;
  cursor: pointer;
  transition: 300ms ease;
}

.wrapper button:hover {
  transform: scale(1.1) ;
}

</style>
