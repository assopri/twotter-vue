<template>
  <div id="user-profile">
{{state.user.username }} - {{fullName}}
<div v-if="state.user.isAdmin">admin</div>
<div v-else>not admin</div>
<strong>Followers : </strong> {{followers}}
<button @click="followUser">Follow</button>
    </div>
    
    <!-- <form class="user-profile__create-form" @submit.prevent="createNewTwoot">
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
      </form> -->
      
<CreateTwootPanel @add-twoot="addTwoot" />

    <div class="user-profile__twoots-wrapper">
    
    <TwootItem 
      v-for="twoot of state.user.twoots" 
      :key="twoot.id" 
      :username="state.user.username" 
      :twoot="twoot" 
      @favourite="toggleFavourite"
    />

        </div>
</template>

<script>
import TwootItem from "./TwootItem";
import CreateTwootPanel from "./CreateTwootPanel";
import {reactive, computed, watch, ref} from "vue";
export default {
  name: 'UserProfile',
  components: {CreateTwootPanel, TwootItem},
  setup()
  {
    const followers = ref(0)
    const state = reactive({
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
    })
    watch(followers, (newValue, oldValue) => 
    {
      if(oldValue < newValue){
            console.log(`${state.user.username} gained follower`)
          }
    })
    const fullName = computed(()=>
      {
          `${state.user.firstName} ${state.user.LastName}`
      })
      function addTwoot(twoot)
            {
                state.user.twoots.unshift({id: state.user.twoots.length+1, content: twoot.text})
            }
            function    toggleFavourite(id, msg)
    {
      console.log(`${msg} tweet ${id}`)
    }
    function followUser()
    {
      followers.value ++;
    }
    return{state,fullName, addTwoot,toggleFavourite,followUser, followers};
  }
}
//  ,
//   computed:{
//     fullName(){
//       return `${this.user.firstName} ${this.user.LastName}`
//     }
//   },
//   methods: {
    
//             addTwoot(twoot)
//             {
//                 this.user.twoots.unshift({id: this.user.twoots.length+1, content: twoot.text})
//             },
//     logSmth()
//     {
//       console.log(this.newTwootContent)
//     },
//     followUser()
//     {
//       this.followers++;
//     },






    // createNewTwoot()
    // {
    //   if(this.newTwootContent && this.selectedTwootType!=='draft')
    //   {
    //     this.user.twoots.unshift({id: this.user.twoots.length+1,
    //     content: this.newTwootContent});
    //   }
    //   this.newTwootContent = '';
    // }
//   },
//   mounted()
//   {
//     this.followUser();
//   }
// }
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