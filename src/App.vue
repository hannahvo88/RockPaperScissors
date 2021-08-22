

<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<style>

body {
  background: rgba(0, 0, 0, 0.6);
}


#app {
  text-align: center;
  color: white;
  margin-top: 60px;
}
.selection {
  font-size: 10em;
}
.container {
  color: white;
  width: 33%;
  border: 2px solid #6abe5f;
  background: rgba(0, 0, 0, 0.5);
  min-height: 350px;
  margin: 15px;
  padding: 15px;
  border-radius: 5px;
}

h1 {
  color: white;
  font-size: 4.5em;
  text-shadow: 2px 2px 6px rgb(28, 235, 38);
  margin-bottom: 15px;
}

.move-img {
  max-width: 200px;
}
</style>