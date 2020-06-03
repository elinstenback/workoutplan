<template>
  <div id="app">
    <h1>workout plan</h1>
    <img alt="Person that works out" src="./assets/background01.jpg">
    <PostComponent />
  </div>
</template>

<script>
import PostComponent from './components/PostComponent.vue'

export default {
  name: 'App',
  components: {
    PostComponent
  }
}
</script>

<style>
body {
  padding: 0;
  margin: 0;
  background-color: #fff;
  text-align: center;
  font-family: 'Muli', arial, sans-serif;
}

h1 {
  background-color: #000;
  color: #fff;
  padding: 20px 0;
  margin: 0 auto;
  text-transform: lowercase;
  font-size: 22px;
  font-weight: 700;
  letter-spacing: 2px;
  max-width: 700px;
}

img {
  max-width: 700px;
  width: 100%;
}

@media only screen and (max-width: 1024px) {
  h1 {
  max-width: 800px;
}
img {
  max-width: 800px;
  width: 100%;
}
}
</style>
