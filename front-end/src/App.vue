<template>
<div id="app">
  <div class="header">
    <router-link to="/">
      <div class="logo">
        <img src="/poke.png">
      </div>
    </router-link>
    <router-link class="page2"  to="/admin">Edit Pokemon List</router-link>
    <router-link to="/">
      <div class="title">
        <h1 class="header"><u>Pokedex Application</u></h1>
      </div>
    </router-link>

  </div>
  <div class="content">
    <router-view />
  </div>
  <div class="footer">
    <a href="https://google.com">My Github Repo</a>
  </div>
</div>
</template>

<style>
html {
  box-sizing: border-box;
}

body {
  font-family: 'Montserrat', sans-serif;
  font-size: 16px;
  background: #c9c9c9;
  padding: 0px;
  margin: 0px;
}

/* Header */
.header {
  display: flex;
  padding: 10px 100px 0px 100px;
  background-cd: black;
  background-color: red;
  color: white;
}

.title {
  margin-top: 5px;
}

.title h1 {
  font-size: 30px;
}

.content {
  padding: 20px 100px;
  min-height: 500px;
}

/* Footer */
.footer {
  height: 50px;
  padding: 20px 100px 0px 100px;
  background: darkgrey;
  font-size: 12px;
}

.footer a {
  color: #000;
}

h1 {
  font-size: 20px;
}

h2 {
  font-size: 14px;
}

.page2{
  margin-top: 100px;
  color: white;
}
</style>
