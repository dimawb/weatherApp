<template>

  <div id="screen">
    <input type="text" v-model="inp" @keydown.enter="press" id="inp" >
    <div id="weather">{{ text_weather }}</div>
    <div id="temp"> {{ text_temp }}</div>
    <div id="speed">{{ text_speed }}</div>
    <div id="humidity">{{ text_humidity }}</div>
    
    <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@24,400,0,0&icon_names=heat" />
    <span class="material-symbols-outlined" id="humidity_icon" v-if="isTrue">
      heat
    </span>
    <div id="text_humidity" v-if="isTrue">Humidity</div>
    

    <img src="./components/icons/wind.png" id="wind_icon" v-if="isTrue">

    <div id="text_wind" v-if="isTrue">Wind speed</div>
    </div>

</template>

<script>
export default{
  data(){
    return{
      inp:'',
      text_weather:'',
      text_temp: '',
      text_speed: '',
      isTrue:true,
      text_humidity:'',
      isTrue:false
    }
  },
  methods: {
     async press(){
      let apikey = '7b614683c2471e0714b175f8c8835f56' 
      let response = await fetch(`https://api.openweathermap.org/data/2.5/weather?q=${this.inp}&appid=${apikey}&units=metric&lang=ru`)
      
      if(!response.ok){
        alert('wrong city name')
      }

      let data = await response.json()
      console.log(data)
      let weather = data.weather[0].description;
      let temp = Math.floor(data.main.temp)
      let speed = Math.floor(data.wind.speed)
      let humidity = data.main.humidity
      this.text_speed = speed + 'km/h'
      this.isTrue = true
      this.text_temp = temp + '°C'
      this.text_humidity = humidity + '%'
      this.text_weather = weather
      this.inp = ''
      this.isTrue = true
     }
  },
}
</script>

<style>
body{
  background-image: url('./components/icons/img_bg.png');
  background-size: 1400px;
  
}
#screen{
    position: absolute;
    height: 400px;
    width: 265px;
    border-radius: 25px;
    left: 40%;
    top: 35%;  
    max-width: 100%;
    max-height: 100%;
	  background-size: 400% 400%;
    background-color: rgba(255, 255, 255, .2);
    
  }
  #inp{
    margin-bottom: 1%;
    height: 37px;
    width: 220px;
    margin-left: 8.5%;
    margin-top: 30%;
    border-radius: 15px;
    border: none;
    outline: none;
    font-size: 15px;
  }
  #temp{
    font-weight: 700;
    font-size: 65px;
    font-family: "Gill Sans", sans-serif;
    margin-left: 25%;
    margin-top: 20%;
  }
  #weather{
    font-size: 19px;
    position: absolute;
    top: 250px;
    left: 80px;
    font-family: "Gill Sans", sans-serif;
  } 
  #humidity_icon{
    position: absolute;
    margin-top: -18%;
    font-size: 40px;

  }
  #text_humidity{
    font-size: 12px;
    margin-top: -17%;
    margin-left: 14%;
  }
  #humidity{
    font-size: 13px;
    position: absolute;
    top: 370px;
    left: 36px;
  }

  #wind_icon{
    position: absolute;
    width: 40px;
    height: 40px;
    margin-top: -5%;
    margin-left: 60%;
  }
  #text_wind{
    margin-left: 73%;
    margin-top: -5%;
    font-size: 12px;
  }
  #speed{
    margin-left: 73%;
    margin-top: 100px;
    margin-left: 196px;
  }
</style>
