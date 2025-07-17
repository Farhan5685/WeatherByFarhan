<template>
    <div class="rain-wrapper">
      <div
        class="raindrop"
        v-for="i in 50"
        :key="i"
        :style="{
          left: `${Math.random() * 100}%`,
          animationDuration: `${Math.random() * 2 + 2}s`,
          animationDelay: `${Math.random() * 2}s`,
          opacity: `${Math.random() * 0.5 + 0.3}`
        }"
      ></div>
    </div>
  </template>
  
  <script setup>
  </script>
  
  <style scoped>
  .rain-wrapper {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    pointer-events: none;
    overflow: hidden;
    z-index: 1; 
  }
  
  .raindrop {
    position: absolute;
    top: -10%;
    width: 2px;
    height: 14px;
    background: rgba(255, 255, 255, 0.3);
    animation: rainFall linear infinite;
    border-radius: 50%;
  }
  
  @keyframes rainFall {
    0% {
      transform: translateY(0);
    }
    100% {
      transform: translateY(120vh);
    }
  }
  </style>
  