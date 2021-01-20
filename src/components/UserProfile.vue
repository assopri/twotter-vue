<template>
  <div id="user-profile">
{{user.username }} - {{fullName}}
<div v-if="user.isAdmin">admin</div>
<div v-else>not admin</div>
<strong>Followers : </strong> {{followers}}
<button @click="followUser">Follow</button>
    </div>
    
    <form class="user-profile__create-form" @submit.prevent="createNewTwoot">
<label for="NewTwoot">New Twoot</label>
<textarea id="NewTwoot" columns="4" v-model="newTwootContent"></textarea>
<div class="user-profile__create-twoot-type">
<label for="NewTwoot">Type</label>
<select id="NewTwoot" v-model="selectedTwootType">
<option :value="option.value" v-for="(option, index) in twootTypes" :key="index" >
  {{option.name}}
  </option>
</select>
</div>
<button>Twoot</button>
      </form>
      

      <!-- <form  @submit.prevent="logSmth">
<select v-model="selectedTwootType">
<option :value="option.value" v-for="(option,index) in twootTypes" :key="index">
{{option.name}}
  </option>
 
  </select>
   <button id="asdf">adf</button>
        </form> -->
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
      newTwootContent: 'def',
      selectedTwootType: 'instant',
      twootTypes:[
        {value: 'draft', name: 'Draft'},
        {value: 'instant', name: 'Instant'}
      ],
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
    logSmth()
    {
      console.log(this.newTwootContent)
    },
    followUser()
    {
      this.followers++;
    },
    toggleFavourite(id, msg)
    {
      console.log(`${msg} tweet ${id}`)
    },
    createNewTwoot()
    {
      if(this.newTwootContent && this.selectedTwootType!=='draft')
      {
        this.user.twoots.unshift({id: this.user.twoots.length+1,
        content: this.newTwootContent});
      }
      this.newTwootContent = '';
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