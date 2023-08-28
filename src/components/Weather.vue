<template>
  <div class="container">
    <div class="box-container" 
        :class="this.temp < 25 ? 'box-background-cold' : 'box-background-warm'" >
      <div class="input-container">
        <input type="text" placeholder="Location" v-model="search" v-on:keyup.enter="getWeather">
        <button v-on:click="getWeather" ><i class="ri-search-line"></i></button>
      </div>
      
      
      <div class="temp-container">
        <h1>{{temp}}°C</h1>
        <span >Feel's Like : {{ feelsLike }}°C</span>

        <div class="date-location">
          <h2>{{location}}</h2>
          <h3>{{date}}</h3>
      </div>
        
        <div class="weather-type">
          <div class="part-1">
            <h2>{{weather}}</h2>
          </div>
          <div class="part-2">
            <h3><i class="ri-windy-line"></i> Wind : {{ windS }} Km/h</h3>
            <h3><i class="ri-water-percent-line"></i> Humidity : {{ humidity }}%</h3>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Weather-a',
  data(){
    return{
      apiKey:"e50b812bfc1b09b7849cc571a0cdf630",
      search:"",
      temp:"00",
      weather:"Weather",
      location:"City Country",
      date:"Date",
      feelsLike:"22",
      windS:"0",
      humidity:"100",
    }
  },
  methods:{
    getWeather(){
      fetch(`https://api.openweathermap.org/data/2.5/weather?q=${this.search}&appid=${this.apiKey}&units=metric`)
                    .then(response=> response.json())
                    .then(this.setData);
    },
    setData(results){
      let wData= results;
      this.temp = wData.main.temp;
      this.feelsLike = wData.main.feels_like;
      this.location = wData.name + " "+ wData.sys.country;
      this.weather = wData.weather[0].main;
      this.windS = wData.wind.speed;
      this.humidity = wData.main.humidity;
      this.date = this.getDateData();
    
      this.search="";
      
    },
    getDateData(){
      let allIn = new Date();
      let months = ['January','February','March','April', 'May', 'June',
                  'July', 'August', 'September', 'October', 'November', 'December'];
      let day = allIn.getDate();
      let month = months[allIn.getMonth()];
      let year = allIn.getFullYear();
      return `${day} ${month} ${year}`;
    }
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container{
  position: absolute;
  width: 100%;
  height: 100vh;
  display:flex;
  justify-content: center;
  background-color: #B9B4C7;
  color: white;
  border: none;
}
.box-container {
  height: 70vh;
  width: 500px;
  max-width: 500px;
  border: 1px solid rgba(0, 0, 0, 0.584);
  box-shadow: 0px 0px 20px 2px rgba(0, 0, 0, 0.482);
  border-radius: 30px;
  overflow: hidden;
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 100px;
  transition: all 1s ease;
}
.box-background-warm{
  background: linear-gradient(180deg, #FFBA86, #F6635C);
  transition: all 1s ease;
}
.box-background-cold{
  background: linear-gradient(180deg, #05BFDB, #0A4D68);
  transition: all 1s ease;
}


.input-container{
  width: 460px;
  margin: 30px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 25px;
  overflow: hidden;
  box-shadow: 0px 0px 2px 1px rgb(65, 65, 65);
  background-color: white;
  
}
.input-container:hover{
  box-shadow: 0px 0px 20px 2px rgba(54, 53, 53, 0.427);
}
.input-container input{
  width: 100%;
  border: none;
  color: #183D3D;
  height: 70px;
  padding: 0px 0px;
  cursor: text;
  font-size: 20px;
  padding: 0px 30px;
  outline: none;
}
.input-container button{
  width: 20%;
  height: 100%;
  border: none;
  font-size: 16px;
  cursor: pointer;
  transition: all 0.3s ease;
  border-radius: 20px;
  background-color: white;
}
.input-container button:hover{
  background-color: rgb(47, 158, 255);
  font-size: 22px;
  transition: all 0.3s ease;
}
.temp-container{
  width: 100%;
  height: 100%;
  text-align: center;
}
.temp-container h1{
  font-family: 'Kanit', sans-serif;
  font-size: 80px;
  margin-bottom: 0px;
  font-weight: 400;
}
.temp-container span{
  font-family: 'Poppins', sans-serif;
  font-size: 18px;
}
.weather-type{
  width: 100%;
  height: 170px;
  font-family: 'Poppins', sans-serif;
  display: flex;
  justify-content: space-evenly;
}
.part-1{
  width: 50%;
  display: flex;
  justify-content: center;
  padding-top: 32px;

}
.part-2{
  width: 50%;
  display: flex;
  flex-direction: column;
  text-align: left;
  justify-content: space-evenly;
}
.part-2 h3{
  font-weight: 200;
  display: flex;
  align-items: center;
}
.part-2 i{
  padding-right: 5px;
  font-size: 30px;
}
.date-location{
  width: 100%;
  margin: 0px 0px;
  text-align: center;
  
}
.date-location h2{
  margin: 0px auto;
  font-family: 'Kanit', sans-serif;
  font-size: 30px;
  
}
.date-location h3{
  margin: 0px auto;
  font-family: 'Kanit', sans-serif;
  font-weight: 100;
  
  
}
</style>
