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
          methods:
          {
            favouriteTwoot(id)
            {
                this.$emit('favourite', id)
            }
          }
      }
      </script>