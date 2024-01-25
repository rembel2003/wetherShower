<script>

import axios  from "axios";
export default {
  data(){
    return{
      city: "",
      error: "",
      info: null
    }
  },
  computed:{
    cityName(){
      return `<<${this.city}>>`

      },
    cityTemp(){
      return `Температура в городе - ${this.info.temp}`
    },
    cityTempLike(){
      return `Ощущается как - ${this.info.feels_like}`
    },
    cityTempMin(){
      return `Минимальная температура- ${this.info.temp_min}`
    },
    cityTempMax(){
      return `Максимальная температура- ${this.info.temp_max}`
    }
  },
  methods:{
    getWeather(){
      if(this.city.trim().length<2){
        this.error ="Введите название корректно"
        return false
      }
      this.error =''

      axios.get('https://api.openweathermap.org/data/2.5/weather?q='+this.city+'&units=metric&APPID=b9a04a4e1434cb41785ddd92e0ab9854')
          .then(response=>(this.info=response.data.main))
    }
  }
}
</script>

<template>
  <div class="wrapper">
    <h1>Погодное приложение</h1>
    <p>Узнать погоду в {{city == ''?"вашем городе":cityName}}</p>
    <input type="text" v-model="city" placeholder="Введите город" >
    <button v-if="city !==''" @click="getWeather()">Узнать погоду</button>
    <p class="error">{{error}}</p>
    <div v-if="info != null">
      <p>{{cityTemp}}</p>
      <p>{{cityTempLike}}</p>
      <p>{{cityTempMin}}</p>
      <p>{{cityTempMax}}</p>
    </div>
  </div>
</template>

<style scoped>
.error{
  color: red;
}
.wrapper {
  width: 900px;
  height: 500px;
  border-radius: 50px;
  padding: 20px;
  background: #1f0f24;
  text-align: center;
  color: white ;
}
.wrapper h1 {
 margin-top: 50px;
}
.wrapper p{
  margin-top: 20px;
}
.wrapper input{
  margin-top: 30px;
  background: transparent;
  border:0;
  border-bottom: 2px solid #110813;
  color: #FCFCFC;
  padding:5px 8px ;
  font-size: 14px;
  outline: none;
}
.wrapper input:focus{
  border-bottom-color: #6e2de7;
}
.wrapper button{
  background: #e3bc4b;
  color: #FCFCFC;
  border-radius: 10px;
  border: 2px solid #b99935;
  padding: 10px 15px;
  margin-left: 20px;
  cursor: pointer;
  transition: transform 500ms ease;
}
.wrapper button:hover{
  transform: scale(1.1) translateY(-5px);
}
</style>
