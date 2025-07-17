<template>
    <v-card class="pa-4 weather-card" elevation="10">
      <v-row>
        <v-col cols="12" md="6">
          <h2 class="text-h5 mb-2">{{ weather.name }}</h2>
          <p class="text-h6 text-capitalize">
            {{ weather.weather[0].description }}
          </p>
          <v-icon size="64" class="my-2">
            {{ icon }}
          </v-icon>
        </v-col>
        <v-col cols="12" md="6">
          <p>🌡 Temperature: <strong>{{ weather.main.temp }}°C</strong></p>
          <p>💧 Humidity: <strong>{{ weather.main.humidity }}%</strong></p>
          <p>🌬 Wind Speed: <strong>{{ weather.wind.speed }} m/s</strong></p>
        </v-col>
      </v-row>
    </v-card>
  </template>
  
  <script setup>
  defineProps({
    weather: Object,
    icon: String,
  })
  </script>
  
  <style scoped>
  .weather-card {
    border-radius: 16px;
    transition: transform 0.3s ease;
    background-color: rgba(34, 32, 32, 0.856);
    color:white
  }
  .weather-card:hover {
    transform: scale(1.02);
  }
  </style>
  