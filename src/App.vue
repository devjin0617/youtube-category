<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <div style="text-align:center;">
      <button @click="login">로그인</button>
    </div>
    <router-view/>
  </div>
</template>

<script>
export default {
  mounted () {
    // this.$Loading.start()
  },
  methods: {
    login () {
      const clientId = ''
      const url = `https://accounts.google.com/o/oauth2/auth?client_id=${clientId}&redirect_uri=http://localhost:8080/oauth2callback&scope=https://www.googleapis.com/auth/youtube.readonly&response_type=token`
      location.href = url
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#nav {
  padding: 30px;
  a {
    font-weight: bold;
    color: #2c3e50;
    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
