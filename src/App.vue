<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
<div class="app">
 <header class="header">
  <div class="header-body">
    <div class="header-logo">
    <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="50" height="50" />
    <h2>AG && MT</h2>
  </div>
      <nav class="header-nav">
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/purchases">Purchases</RouterLink>
        <RouterLink to="/gallery">Gallery</RouterLink>
      </nav>
    </div>
  </header>

  <div class="container">
 <RouterView />
  </div>
  
</div>
</template>


<style>
@import './assets/base.css';
#app {

  width: 100%;
}
.header{
  margin: 2rem;
  height: 100px;
  border-radius: 12px;
  box-shadow: 0 0 9px rgba(19, 31, 19, 0.4) ;
  background: #fff;
}
.header-logo{
  display: flex;
  align-items: center;
}
.header-body{
  padding: 0 15px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 100%;
  width: 100%;
}
.header-nav a{
  font-size: 17px;
  text-decoration: none;
  color: rgba(19, 22, 31, 0.55);
  margin: 0 10px;
}
.header-nav a:hover{
  color: rgb(36, 110, 77);
  border-bottom: 1px solid rgb(52, 213, 140);
  
}

</style>
