<template>
  <div id="twoot-item" @click="favouriteTwoot(twoot.id)">
      <div class="user-profile__twoot">
            
        <br >
        <div class="twoot-item__user">
            @{{username}}
        </div>
        <div class="twoot-item__content">
            @{{twoot.content}}
        </div>   
        <div v-if="favourited"  class="twoot-item__favourited">
            favourited
        </div>   
            
        <br > 
      </div>
  </div>
</template>
<script>

      export default {
          name: "TwootItem",
          props:{
              username: {
                  type: String,
                  required: true
              },
              twoot:{
                  type: Object,
                  required: true
              }
          },
          data(){
              return {
                  favourited : false
              }
          },
          methods:
          {
            favouriteTwoot(id)
            {          
                let msg = (this.favourited?"de":"") + 'favourite';
                
                this.$emit('favourite', id, msg)
                this.favourited = !this.favourited;
            }
          }
      }
      </script>