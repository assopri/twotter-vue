<template>
  <div id="user-profile">
{{user.username }} - {{fullName}}
<div v-if="user.isAdmin">admin</div>
<div v-else>not admin</div>
<strong>Followers : </strong> {{followers}}
<button @click="followUser">Follow</button>
    </div>
    <div class="user-profile__twoots-wrapper">
    
    <TwootItem 
      v-for="twoot of user.twoots" 
      :key="twoot.id" 
      :username="user.username" 
      :twoot="twoot" 
      @favourite="toggleFavourite"
    />

        </div>
</template>

<script>
import TwootItem from "./TwootItem";

export default {
  name: 'UserProfile',
  components: {TwootItem},
  data(){
    return {
      followers: 0,
      user: {
        id: 1,
        username: "_MitchelRomney",
        firstName: 'Mitchel',
        LastName: 'Romney',
        email: 'mitc@m.com',
        isAdmin: false,
        twoots: [
            {id: 1, content:'Twotter is cool'},
            {id: 2, content: "subscribe"}
        
        ]
      }
    }
  },
  watch:{
    followers(newFollowerCount, oldFollowerCount)
    {
      if(oldFollowerCount < newFollowerCount){
        console.log(`${this.user.username} gained follower`)
      }
    }
  },
  computed:{
    fullName(){
      return `${this.user.firstName} ${this.user.LastName}`
    }
  },
  methods: {
    followUser()
    {
      this.followers++;
    },
    toggleFavourite(id, msg)
    {
      console.log(`${msg} tweet ${id}`)
    }
  },
  mounted()
  {
    this.followUser();
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