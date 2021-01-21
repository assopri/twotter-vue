<template>
  <div id="app">
    <nav>
        <div class="navi__logo">
        Twotter
        </div>
        <div class="navi__user">
        {{user.username}}
        </div><br /><br />
    </nav>
<UserProfile />
    </div>
</template>

<script>
import UserProfile from "./components/UserProfile";

export default {
  name: 'App',
  components: {UserProfile} ,
  data()
  {
    return{
      user:
      {
        username: '_MitchelRomney'
      }
    }
  }
}
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
