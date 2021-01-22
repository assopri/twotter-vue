<template>
  <div id="twoot-item" @click="favouriteTwoot(twoot.id)">
      <div class="user-profile__twoot">
            
        <br >
        <div class="twoot-item__user">
            @{{username}} {{twoot.id}}
        </div>
        <div class="twoot-item__content">
            @{{twoot.content}}
        </div>   
        <div v-if="state.favourited"  class="twoot-item__favourited">
            favourited
        </div>   
            
        <br > 
      </div>
  </div>
</template>
<script>
import {reactive} from "vue";
      export default {
          name: "TwootItem",
          props: {
            twoot : {
                type: Object,
                required: true
            },
            username: {
                type: String,
                required: true
                }
        },
          setup(props,ctx)
            {
               
                console.log(props)
                const state = reactive({favourited:false});

                function favouriteTwoot(id)
                        {       
                            console.log(`keyprop is ${props.twoot.id}`)   
                            let msg = (state.favourited?"de":"") + 'favourite';
                            
                            ctx.emit('favourite', id, msg)
                            state.favourited = !state.favourited;
                            // props.twoot.content +="1";
                        }

                        return {favouriteTwoot, state };
            }
        //   props:{
        //       username: {
        //           type: String,
        //           required: true
        //       },
        //       twoot:{
        //           type: Object,
        //           required: true
        //       }
        //   },
         
      }
      </script>