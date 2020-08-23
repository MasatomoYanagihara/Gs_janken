<template>
  <div id="app">
    <h1 class="title">じゃんけん</h1>
    <h2>モード選択</h2>
    <div id="nav">
      <router-link to="/">Easy</router-link>
      <router-link to="/normal">Normal</router-link>
      <router-link to="/hard">Hard</router-link>
    </div>
    <router-view />
  </div>
</template>

<style>
@import url("https://fonts.googleapis.com/earlyaccess/nicomoji.css");
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#app .title {
  font-family: "Nico Moji";
  font-size: 96px;
  color: #ffcc99;
}

body {
  margin: 0;
}

.title {
  margin: 0 auto 30px;
  padding-top: 30px;
  font-size: 54px;
}

h2 {
  margin: 0 auto;
}

#nav {
  margin-bottom: 40px;
}

#nav a {
  margin: 0 30px;
  font-size: 36px;
  font-weight: bold;
  color: #2c3e50;
  list-style: none;
  text-decoration: none;
}

#nav a.router-link-exact-active {
  color: #42b983;
}

button {
  border: 1px solid black;
}
</style>
