<template>
    <v-app>
      <div class="weather-bg">
        <v-container class="fill-height d-flex align-center justify-center text-center">
          <v-row>
            <v-col cols="12" md="8" class="mx-auto">
              <!-- Heading -->
              <div class="heading-box mb-8">
                <h1 class="app-title">Weather App</h1>
                <p class="subtitle">Get real-time weather with style 😎</p>
              </div>
  
              <!-- Form Style Card -->
              <v-card class="form-glass pa-6" elevation="12" rounded="xl">
                <v-text-field
                  v-model="city"
                  label="Enter city"
                  variant="outlined"
                  class="mb-4"
                  prepend-inner-icon="mdi-map-marker"
                  @keyup.enter="fetchWeather"
                  :loading="loading"
                  clearable
                  color="cyan"
                />
  
                <v-btn
                  block
                  color="cyan-darken-1"
                  class="glow-btn"
                  size="large"
                  :disabled="!city"
                  @click="fetchWeather"
                >
                  Get Weather
                </v-btn>
  
                <!-- Result -->
                <WeatherCard
                  v-if="weather"
                  :weather="weather"
                  :icon="weatherIcon"
                  class="mt-6"
                />
  
                <!-- Error -->
                <v-alert
                  v-if="error"
                  type="error"
                  variant="tonal"
                  border="start"
                  class="mt-4"
                >
                  {{ error }}
                </v-alert>
                <p class="pt-5">Made By Farhan.Dev</p>
              </v-card>
            </v-col>
          </v-row>
        </v-container>
      </div>
    </v-app>
    
  </template>
  
  <script setup>
  import { ref, computed } from 'vue'
  import WeatherCard from '@/components/WeatherCard.vue'
  
  const city = ref('')
  const weather = ref(null)
  const loading = ref(false)
  const error = ref('')
  
  const API_KEY = '86d7869048b27624164533c00e598084'
  
  const fetchWeather = async () => {
    if (!city.value) return
    loading.value = true
    error.value = ''
    weather.value = null
  
    try {
      const res = await fetch(
        `https://api.openweathermap.org/data/2.5/weather?q=${city.value}&appid=${API_KEY}&units=metric`
      )
      if (!res.ok) throw new Error('City not found!')
      weather.value = await res.json()
    } catch (err) {
      error.value = err.message
    } finally {
      loading.value = false
    }
  }
  
  const weatherIcon = computed(() => {
    if (!weather.value) return 'mdi-weather-cloudy'
    const type = weather.value.weather[0].main.toLowerCase()
    if (type.includes('cloud')) return 'mdi-weather-cloudy'
    if (type.includes('rain')) return 'mdi-weather-rainy'
    if (type.includes('clear')) return 'mdi-weather-sunny'
    if (type.includes('snow')) return 'mdi-weather-snowy'
    return 'mdi-weather-partly-cloudy'
  })
  </script>
  
  <style scoped>
  .weather-bg {
    min-height: 100vh;
    background: #000;
    padding-top: 60px;
    padding-bottom: 40px;
  }
  
  .heading-box {
    text-align: center;
  }
  
  .app-title {
    font-size: 2.8rem;
    font-weight: bold;
    color: #00bcd4;
    text-transform: uppercase;
    letter-spacing: 2px;
  }
  
  .subtitle {
    color: #bbb;
    font-size: 1.1rem;
  }
  
  .form-glass {
    background: rgba(24, 24, 24, 0.9);
    border-radius: 20px;
    border: 1px solid rgba(255, 255, 255, 0.06);
    box-shadow: 0 0 30px rgba(0, 188, 212, 0.2);
    color: white;
  }
  
  .glow-btn {
    font-weight: bold;
    transition: all 0.3s ease;
    box-shadow: 0 0 10px rgba(0, 188, 212, 0.4);
  }
  .glow-btn:hover {
    box-shadow: 0 0 18px rgba(0, 188, 212, 0.7);
  }
  </style>
  