<template>
  <div id="app">
    <Header></Header>
    <router-view/>
  </div>
</template>

<script>
import Header from './components/Header'

export default {
  name: 'App',
  components: { Header }
}
</script>

<style>
body{
  margin: 0;
  font-family: "Nunito", sans-serif;
}
h3,h2,h1{
  margin-top: 0;
  margin-bottom: 0.5rem;
  font-weight: 500;
  line-height: 1.2;
}
@media (min-width: 1200px) {
  h3 {
    font-size: 1.575rem;
  }
}
</style>
