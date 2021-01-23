<template>
  <div class="home">
    <h1>Home</h1>
    <router-link v-for="user in users" :key="user.userId" :to="{name: 'UserProfile', params: {userId: user.userId}}">
        {{user.username}}<br />
      </router-link>
  </div>
</template>

<script>
// @ is an alias to /src
import {users} from "../assets/users"

export default {
  name: 'Home',
  setup()
  {
    return{users};
  }
}
</script>
