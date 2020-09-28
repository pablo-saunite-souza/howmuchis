<template>
  <div id="app">
    <div class="container pt-3">
      <h1>How Much Is</h1>
      <h3>Your better online currency conversor</h3>
    </div>
    <div id="dashboard" class="container">
      <div class="d-flex row justify-content-center align-items-center">
        <Conversor />
      </div>
    </div>
    <div class="card mt-2 shadow bg-white rounded fixed-bottom">
      <div class="card-body">
        <h5 class="card-title">How Much is</h5>
        <p class="card-text">
          Donate: my Acounts...
        </p>
        <p class="card-text">
          <small class="text-muted">Copyright 2020 - ©howmuchis<br>Powered by Pablo Saunite de Souza.</small>
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import "bootstrap/dist/css/bootstrap.css";
import "font-awesome/css/font-awesome.css";
import Conversor from "./components/Conversor.vue";

export default {
  name: 'App',
  components: {
    Conversor
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: #ddd;
  width: 100vw;
  height: 100vh;
}

.container {
  margin-left: auto;
  margin-right: auto;
  margin-top: auto;
  margin-bottom: auto;
}

</style>