<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <p>
      {{ message }}
    </p>
    <p>
      {{ date }}
    </p>
    <input type="text" v-model="name" @keyup="getUserInfo" />
    <p v-if="grettings">
      {{ grettings }}
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
      name: "",
      grettings: null,
      timer: null,
    };
  },
  created() {
    setInterval(() => {
      this.date = new Date();
    }, 1000);
  },
  methods: {
    async getUserInfo() {
      clearTimeout(this.timer);

      this.timer = setTimeout(async () => {
        this.grettings = null;

        if (this.name.length <= 3) {
          return;
        }

        const res = await fetch(`https://api.agify.io/?name=${this.name}`);
        const result = await res.json();

        this.grettings = `Hola, ${result.name}. Tu nombre tiene ${
          result.age || 0
        } años.`;
      }, 300);
    },
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
