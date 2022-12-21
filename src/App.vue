<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <p>
      {{ message }}
    </p>
    <p>
      {{ date }}
    </p>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      message: "Welcome to Lolocar",
      date: new Date(),
    };
  },
  created() {
    setInterval(() => {
      this.date = new Date();
    }, 1000);
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
