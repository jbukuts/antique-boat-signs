<template>
  <div id="app">
    <div id="nav">
      <h2>Antique Boat Signs</h2>
      <div id="pages">
        <router-link to="/">Home</router-link>
        <router-link to="/about">About</router-link>
      </div>
    </div>

    <transition name="fade" mode="out-in">
      <router-view/>
    </transition>
  </div>
</template>

<style>

html {
  height: 100%;
  font-size: 100%;
}

body {
  border: 0px;
  margin: 0px;
  padding: 0px;
  height: 100%;
  font-size: 100%;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  background-color: rgb(52, 56, 114);
  width: 100%;
  padding-top: 20px;
}

#pages {
 text-align: center;
 width: 100%;
 background: rgb(53, 53, 53);
 margin: auto;
 text-align: center;
 padding-top: 5px;
 padding-bottom: 5px;
}

#pages > a {
  margin-right: 5px;
  margin-left: 5px;
}

h2 {
  color: #ffffff;
  text-align: center;
  margin-bottom: 20px;
  font-size: 32px;
  font-weight: normal;
  font-family: 'Brush Script Std';
}

#nav a {
  font-weight: bold;
  color: #ffffff;
  text-decoration: none;
  font-weight: normal;
}

#nav a.router-link-exact-active {
  color: #ffffff;
  text-decoration: underline;
}

.fade-enter-active,
.fade-leave-active {
  transition-duration: 0.15s;
  transition-property: opacity;
  transition-timing-function: ease;
}

.fade-enter,
.fade-leave-active {
  opacity: 0
}


</style>
