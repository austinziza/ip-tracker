<template>
  <router-view/>
</template>

<style>
body{
  background-color: lightgrey;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  background-color: #5e5ed4;
  color: #2c3e50;
  height: 400px;
}
@media (min-width: 320px) and (max-width: 760px) {
#app{
  height: 600px;
}
}
</style>
