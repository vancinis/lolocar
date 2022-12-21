<template>
  <div id="app">
    <div>
      <div class="block grid-cols-2 gap-x-4 md:grid my-2">
        <div>
          <p>
            {{ message }}
          </p>
        </div>

        <div>
          <input
            class="px-4 bg-gray-200 rounded-md"
            type="text"
            v-model="name"
            @keyup="getUserInfo"
          />
          <p v-if="grettings">
            {{ grettings }}
          </p>
        </div>
      </div>

      <p>
        {{ date }}
      </p>
    </div>
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
