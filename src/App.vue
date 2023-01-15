<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<style>

/*  DEFAULTS # */
*, *:before, *:after {
  box-sizing: inherit;
  margin: 0;
  padding: 0;
}

html {
  box-sizing: border-box;
  font-size: 16px;
  font-family: proxima-nova;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: #F3F6F9;
}

</style>
