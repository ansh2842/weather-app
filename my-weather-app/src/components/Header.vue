<template>
  <div class="flex w-full justify-between items-center heads">
    <div class="bg-white/30 backdrop-blur-md rounded-md shadow-md w-80 h-90 grid justify-center mb-60 ml-20 p-6 main">
      <h1 class="text-3xl text-black-500 mb-4">Weather App</h1>

      <div class="w-full max-w-sm flex items-center">
        <div class="relative flex-1">
          <input v-model="city" @input="filterCities" class="appearance-none bg-transparent border-none w-full text-gray-700 mr-3 py-1 px-2 leading-tight focus:outline-none" type="text" placeholder="Enter city" aria-label="City">
          <ul v-if="showFilter" class="absolute z-10 bg-white w-full mt-1 rounded-md shadow-lg">
            <li v-for="city in filteredCities" :key="city" @click="selectCity(city)" class="py-1 px-3 hover:bg-gray-100 cursor-pointer">{{ city }}</li>
          </ul>
        </div>
        <button @click="fetchWeather" class="flex-shrink-0 border-none text-gray-700 py-1 px-2 focus:outline-none">
          <i class="fas fa-search"></i>
        </button>
      </div>
    </div>

    <div v-if="weather" class="data bg-white/30 backdrop-blur-md mt-4 text-center w-80 relative ">
      <h2 class="text-2xl  text-orange">{{ weather.name }}</h2>
      <p class="text-3xl font-bold">{{ weather.main.temp }}°C</p>
      <p class="text-lg text-orange">{{ weather.weather[0].description }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      city: '',
      weather: null,
      cities: ['Delhi','Moscow', 'Paris', 'New York', 'Riyadh', 'Sydney'],
      filteredCities: [],
    };
  },
  computed: {
    showFilter() {
      return this.filteredCities.length > 0 && this.city.trim() !== '';
    }
  },
  methods: {
    async fetchWeather() {
      if (this.city.trim() === '') {
        alert('Please enter a city name');
        return;
      }

      try {
        const response = await fetch(`http://localhost:3000/index/weather?city=${this.city}`);
        const data = await response.json();
        if (response.ok) {
          this.weather = data;
        } else {
          alert(data.error || 'Failed to fetch weather data');
        }
      } catch (error) {
        console.error('Error fetching weather data:', error);
        alert('Error fetching weather data');
      }
    },
    filterCities() {
     
      this.filteredCities = this.cities.filter(city => city.toLowerCase().includes(this.city.toLowerCase()));
    },
    selectCity(city) {
      this.city = city;
      this.filteredCities = []; 
    }
  },
  mounted() {
    
    if (this.weather) {
      const weatherCondition = this.weather.weather[0].main.toLowerCase();
      const clouds = document.querySelector('.clouds');
      if (clouds) {
        if (weatherCondition.includes('cloud')) {
          clouds.classList.add('cloudy');
        } else {
          clouds.classList.remove('cloudy');
        }
      }
    }
  }
};
</script>

<style scoped>
.data {

  position: relative;
  left:12rem;
  width:300px;
  height:400px;
 border-radius:7px;
  background-image: url('../image/clouds-transparent-background-75.png');
  animation: cloudsAnimation 60s linear infinite; 
    background-size: cover;
  z-index: -1;
  pointer-events: none;
  opacity: 1; 
   display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  color: white;
}


@keyframes cloudsAnimation {
  0% { background-position: 0 0; }
  100% { background-position: 100% 0; }
}
@media screen and (max-width: 640px) {
  .main {
  position: relative;
    left: -50px;
    margin-top: 11rem;
  }
  .heads{
  display: inline-block;
  }
  .data{
  position: relative;
  left:38px;
  bottom: 177px;
  }
  

}
</style>
